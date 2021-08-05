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
