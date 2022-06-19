# Head

If you wanna add latex formula in Blog with Markdown, add code block below at the head of Markdown file.

```html
<head>
    <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
    <script type="text/x-mathjax-config">
        MathJax.Hub.Config({
            tex2jax: {
            skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
            inlineMath: [['$','$']]
            }
        });
    </script>
</head>
```

Insert a picture in the text and center it

```html
<div align=center>
    <img src="source" width="300"/>
</div>
```

Text background color settings

```html
<table><tr><td bgcolor="gray">TEXT</td></tr></table>
```

pdf

```html
<iframe src="https://authurwhywait.github.io/pdfs/fourier.pdf" style="width:95%; height:1300px;" frameborder="0"></iframe>
```

comments

```html

<link rel="stylesheet" href="//unpkg.com/gitalk/dist/gitalk.css">
<script src="//unpkg.com/gitalk/dist/gitalk.min.js"></script>
<div id="gitalk-container"></div>
<script>
    var gitalk = new Gitalk({
        clientID: 'c5997a4ef68d75e658c7',
        clientSecret: '77b8fd83267599e9f0eae497ba480d50764142c0',
        repo: 'blog-comments',
        owner: 'AuthurWhywait',
        // admin: ['AuthurWhywait'],
        // title: location.hash.match(/#(.*?)([?]|$)/)[1],
        // id: location.hash.match(/#(.*?)([?]|$)/)[1],
        id: "20220617",
    })
    // 监听URL中hash的变化，如果发现换了一个MD文件，那么刷新页面，解决整个网站使用一个gitalk评论issues的问题。
    // window.onhashchange = function (event) {
    //     if (event.newURL.split('?')[0] !== event.oldURL.split('?')[0]) {
    //         location.reload()
    //     }
    // }
    gitalk.render('gitalk-container')
</script>
```
