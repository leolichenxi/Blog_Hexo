关于使用VertexStreamSplitting优化带宽
方案介绍
Tile-based GPUs create a shader that calculates the normalized device coordinates based on the provided vertex shader to do binning. It is executed first on every vertex in the scene, whether visible or not. Keeping vertex position data contiguous in memory is therefore a big plus. Other places this vertex stream layout can be beneficial is for shadow passes, as usually you only need position data for shadow calculations, as well as depth prepasses, which is a technique usually used for console/desktop rendering; this vertex stream layout can be a win for multiple classes of the rendering engine!
Stream Splitting involves setting up the vertex buffer with a contiguous section of vertex position data and another section containing interleaved vertex attributes. Most applications usually set up their buffers fully interleaving all attributes. This visual explains the difference:

Looking at how the GPU fetches vertex data helps us understand the benefits of stream splitting. Assuming for the sake of argument:
●32 byte cache lines (a pretty common size)
●Vertex format consisting of:Position, vec3<float32> = 12 bytes
○Normal vec3<float32> = 12 bytes
○UV coordinates vec2<float32> = 8 bytes
○Total size = 32 bytes
When the GPU fetches data from memory for binning, it will pull a 32-byte cache line to operate on. Without vertex stream splitting, it will only actually use the first 12 bytes of this cache line for binning, and discard the other 20 bytes as it fetches the next vertex. With vertex stream splitting, the vertex positions will be contiguous in memory, so when that 32-byte chunk is pulled into cache, it will actually contain 2 whole vertex positions to operate on before having to go back to main memory to fetch more, a 2x improvement!
Now, if we combine the vertex stream splitting with vertex compression, we will reduce the size of a single vertex position down to 6 bytes, so a single 32-byte cache line pulled from system memory will have 5 whole vertex positions to operate on, a 5x improvement!
原文链接    https://developer.android.com/games/optimize/vertex-data-management#vertex_stream_splitting

摘要：更改顶点缓存布局，将Position与其他的顶点属性分开处理，使Position属性的内存分布变得连续，从而提高cache命中率，降低带宽与性能开销，配合Vertex Compression 使用，效率会更高

unity当中实现也比较简单，将顶点属性分配到不同的stream中，unity支持4个stream，我们这边用2个就可以了，在工具导出fbx的mesh时为新生成的mesh设置下即可


测试数据
Device：黑鲨 3Pro   GPU:Adreno (TM) 650
测试环境：一定数量的玩家主城白模，顶点数约 45w   FPS：30 

Bandwidth(Bytes/Second)


Original Mesh：R + W  ≈  1.75g
Vertex Stream Splitting Mesh：R + W  ≈  1.35g
带宽降低约400M，主要来自Read带宽

VertexMemoryRead(Bytes/Second)

VertexMemoryRead相差约400M， 对比上一条，可见降低的Read带宽均为VertexMemory

Avg(% Stalled on System Memory)

可以看到StalledOnSystemMemory的百分比下降明显，原因是cache命中率的提高，大大降低了system memory的读取

附录

```
       private static readonly VertexAttributeDescriptor[] vertexAttributeDescriptorList = new[]{
            new VertexAttributeDescriptor(VertexAttribute.Position, VertexAttributeFormat.Float32, 3,0),
            new VertexAttributeDescriptor(VertexAttribute.Normal, VertexAttributeFormat.Float32, 3,1),
            new VertexAttributeDescriptor(VertexAttribute.Tangent, VertexAttributeFormat.Float32, 4,1),
            new VertexAttributeDescriptor(VertexAttribute.Color, VertexAttributeFormat.Float32, 4,1),
            new VertexAttributeDescriptor(VertexAttribute.TexCoord0, VertexAttributeFormat.Float32, 2,1),
            new VertexAttributeDescriptor(VertexAttribute.TexCoord1, VertexAttributeFormat.Float32, 2,1),
            new VertexAttributeDescriptor(VertexAttribute.TexCoord2, VertexAttributeFormat.Float32, 4,1)
        };

        private static Mesh CreateMeshFrom(Mesh mesh)
        {
            Mesh mesh1 = Object.Instantiate(mesh);
             
            //顶点属性分流
       
            //设置顶点属性
            int vertexCount = mesh.vertexCount;
            mesh1.SetVertexBufferParams(vertexCount,vertexAttributeDescriptorList);
            return mesh1;
        }
```



