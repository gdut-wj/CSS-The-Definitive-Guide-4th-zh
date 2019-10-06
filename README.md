# CSS-The-Definitive-Guide-4th-zh

CSS 权威指南第四版 中文翻译

<img src="./cover.png" width=40%>

## 前言

在不知干了多久的 Android 开发和 Java 后端开发后，由于公司需要，开始转行 Web 前端方向。在系统化学习前端知识时候，无奈发现市面上只有《CSS 权威指南（第三版）》的中文版（2007 年 10 月第一版）。众所周知，CSS 的标准发展日新月异，本书的第一章写于 2012 年，现在来看部分内容已经稍有落后，而等到第四版的中文版引入国内时，又不知何年何月了。遂决定阅读英文版，此 repo 仅为个人参考翻译。

英文正式版已于 2017 年 10 月正式出版。

## Index

- [第 1 章 CSS 和 Documents](docs/ch1.md)
- [第 2 章 选择器](docs/ch2.md)
- [第 3 章 特异性和级联](docs/ch3.md)
- [第 4 章 值和单位](docs/ch4.md)
- [第 5 章 字体](docs/ch5.md)
- [第 6 章 文本属性](docs/ch6.md)
- [第 7 章 基本的视觉格式化](docs/ch7.md)
- [第 8 章 Padding, Borders, Outlines 和 Margins](docs/ch8.md)
- [第 9 章 颜色、背景和渐变](docs/ch9.md)
- [第 10 章 浮动和形状](docs/ch10.md)
- [第 11 章 定位](docs/ch11.md)
- [第 12 章 灵活的框布局](docs/ch12.md)
- [第 13 章 网格布局](docs/ch13.md)
- [第 14 章 CSS 中的表格布局](docs/ch14.md)
- [第 15 章 列表和生成的内容](docs/ch15.md)
- [第 16 章 转换 ](docs/ch16.md)
- [第 17 章 跃迁](docs/ch17.md)
- [第 18 章 动画](docs/ch18.md)
- [第 19 章 过滤器，混合，剪切和掩蔽](docs/ch19.md)
- [第 20 章 Media-Dependent 风格](docs/ch20.md)

## 本地开发 & 阅读

本项目基于 vuepress 进行开发，以提供比 github mardown 更佳的阅读体验
依赖于 `node.js`、`yarn`、`vuepress` 等环境

```sh
# node
node -v
> v10.14.1
# yarn
yarn -v
> 1.13.0
# vuepress
yarn global add vuepress

# 本地开发
git clone https://github.com/gdut-yy/CSS-The-Definitive-Guide-4th-zh.git
cd CSS-The-Definitive-Guide-4th-zh
yarn docs:dev

# 本地阅读
http://localhost:8080/
```

## Contributors

<table>
  <tr>
    <td align="center"><a href="https://gdut-yy.github.io/"><img src="https://avatars2.githubusercontent.com/u/33390928?s=460&v=4" width="100px;" /><br /><sub><b>gdut-yy</b></sub></a><br /></td>
    <td align="center"><a href="https://github.com/gdut-wj"><img src="https://avatars3.githubusercontent.com/u/38821031?s=460&v=4" width="100px;" /><br /><sub><b>gdut-wj</b></sub></a><br /></td>
  </tr>
</table>

## License

[MIT](https://github.com/gdut-yy/CSS-The-Definitive-Guide-4th-zh/blob/master/LICENSE)
