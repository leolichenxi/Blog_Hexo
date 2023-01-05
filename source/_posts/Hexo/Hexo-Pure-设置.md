---
title: Hexo Pure主题设置记录
categories: Hexo
tags: pure
date: 2021-06-11 13:43:00
toc: true
---

# Pure 设置记录

新电脑环境设置：
[文档地址](https://github.com/cofess/hexo-theme-pure/blob/master/README.cn.md)

### 背景动态设置
[背景动画](https://link.csdn.net/?target=https%3A%2F%2Fgithub.com%2Fhustcc%2Fcanvas-nest.js) 基于canvas，在\themes\pure\layout\layout.ejs的body中面添加

```

<script type="text/javascript" src="//cdn.bootcss.com/canvas-nest.js/1.0.0/canvas-nest.min.js"></script>

```

### gitcommet 设置

```
comment:
  type: gitment  # 启用哪种评论系统
  # disqus:  # enter disqus shortname here
  # youyan: 
  #   uid: 2kLH6P3hQG2bNQQ9a9mwRFmd-gzGzoHsz # enter youyan uid 
  # livere:
  #   uid: # enter youyan uid 
  gitment:
    githubID: githubname
    repo: githubname.github.io
    ClientID: id
    ClientSecret: secrectid
    lazy: false
```


### 访问数设置
footer.ejs脚本
```
<footer class="footer" itemscope itemtype="http://schema.org/WPFooter">
	<%- partial('_common/social', null, {cache: !config.relative_link}) %>
    <div class="copyright">
    	<% if(theme.site.copyright) { %>
        &copy; <%= date(new Date(), 'YYYY') %> <%= config.author || config.title %>
        <% } %>
    </div>
    <script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>
    <span >本站总访问量: <span id="busuanzi_value_site_pv"></span>次</span>
</footer>
```
