> 网页结构搭建

编码字符集

- UTF-8：万国码
- GBK：汉字字符集

语义化标签

- header
- footer
- nav
- article
- section
- aside
  常规标签
- div
- span

转义字符

vue 中保留字符串中的空格

```vue
<div whitespace-break-spaces>{{ msg }}</div>
<div style="white-space: break-spaces">{{ msg }}</div>
```

a 标签的妙用

```vue
<!-- 拨打电话 -->
<a href="tel:188xxxx7031">联系商家</a>
<!-- 发邮件 -->
<a href="mailto:784884945@qq.com">发送邮件</a>

<!-- 锚点 -->
<div id="point_one">锚点</div>
<a href="#point_one">点击跳转</a>
```

frameset 标签，可以结合 frame 标签进行页面布局和页面跳转（没用）

```html
<frameset cols="20%, 80%">
  <frame src="https://www.jd.com" />
  <frame src="https://www.baidu.com" />
</frameset>
```

iframe 标签，可以在内部引用其他页面，和 framset 基本类似
