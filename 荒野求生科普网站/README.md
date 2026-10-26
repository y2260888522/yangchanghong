# 荒野求生科普网站 · 使用说明

高级网页设计 I　图像解决方案实验作品

---

## 一、文件说明

```
荒野求生科普网站/
├── index.html       主页面（字体图标方案，含 5 项下导航）
├── svg-demo.html    SVG 对照页（技术上与 index 有区别）
├── iconfont/        字体图标文件夹（需你自己放入，见下）
│   ├── iconfont.css
│   ├── iconfont.woff2
│   ├── iconfont.woff
│   └── iconfont.ttf
└── README.md        本说明
```

## 二、三步跑起来

### 第 1 步：准备 iconfont 文件

1. 打开 [iconfont.com](https://www.iconfont.cn/)，登录。
2. 按下列关键词分别搜索图标，加入购物车：

   | 需要的类名 | 搜索关键词 |
   |---|---|
   | `icon-yingji` | 警示 / 警告 / 注意 |
   | `icon-jingshui` | 水滴 / 水 |
   | `icon-quhuo` | 火焰 / 火 |
   | `icon-biyou` | 帐篷 / 露营 |
   | `icon-shouye` | 首页 / 主页 |
   | `icon-sousuo` | 搜索 |
   | `icon-gengduo` | 更多 / 展开 |
   | `icon-ditu` | 地图 / 定位 |
   | `icon-jijiu` | 急救 / 医疗包 / 十字 |
   | `icon-zhinan` | 指南针 / 罗盘 |
   | `icon-shoucang` | 收藏 / 星标 |
   | `icon-fenxiang` | 分享 |
   | `icon-dianhua` | 电话 |

3. 全部加入后，点购物车 → **添加至项目**（新建项目，名字随意）。
4. 进入项目页 → **下载至本地**，解压。
5. 把解压出来的文件夹**重命名为 `iconfont`**，放进本目录（与 `index.html` 同级）。

### 第 2 步：核对类名

iconfont 生成的类名通常是 `icon-` + 图标原名（拼音），**不一定**和我写的一致。打开 `iconfont/demo_index.html`，能看到每个图标的实际类名。

如果你的类名不一样（比如火焰叫 `icon-huoyan` 而不是 `icon-quhuo`），在 `index.html` 里全局替换即可：

- 找 `icon-quhuo` → 替换成 `icon-huoyan`

**建议做法**：先在 iconfont 项目里给每个图标「编辑名称」，直接改成我用的这套（`yingji`、`jingshui`…），这样代码一行都不用改。

### 第 3 步：预览

- **VS Code**：装 Live Server 插件 → 右键 `index.html` → Open with Live Server。
- **或者**直接双击 `index.html`，浏览器也能打开（字体图标需要同目录有 `iconfont` 文件夹）。

## 三、截图作业怎么截（对应报告 3 处占位）

打开 `index.html` 后按 **F12**，点左上角手机图标（Toggle device toolbar）：

| 截图 | 操作 | 报告对应位置 |
|---|---|---|
| 375px 效果图 | 设备选 iPhone SE（375×667） | 实施过程（3）下导航实现图 |
| 1920px 效果图 | 设备选 Responsive，宽度输入 1920 | 同上，第二张 |
| 固定效果验证 | 页面滚动到中部再截，证明导航没动 | 可在图注说明 |

`svg-demo.html` 也可以截一张，放在报告 2.3 节后面作为 SVG 方案的佐证。

## 四、评分点对照

| 评分项 | 本项目对应实现 |
|---|---|
| HTML（1分） | `index.html` 语义化使用 `<nav>`、`<header>`、`<main>`、`<section>`、`<article>`、`<aside>`、`<footer>`；字体图标用 `<i class="iconfont icon-xxx">` 表示 |
| CSS（1分） | 全局 `:root` 变量统一配色；`.wx-tabbar__icon { font-size:22px; color:#8fa698 }` 演示改大小与改颜色；选中态、悬浮态、点按反馈 |
| 字体图标（1分） | 12 个主题定制图标，全部 `wx-` 姓名缩写前缀，无 id 选择器，样式全局化 |
| 整体效果（1分） | 深林绿 + 警示橙配色，主视觉、快捷入口、技能卡、要诀列表层次清晰 |
| 实验报告（1分） | 见已填写的 `.doc` 报告 |

## 五、技术要点速查（答辩可直接用）

### 自适应宽度为什么不用媒体查询？

```css
.wx-tabbar      { display: flex; }
.wx-tabbar__item{ flex: 1 1 0; min-width: 0; }
```

`flex: 1 1 0` 让 5 个子项**忽略内容宽度、按比例等分**容器。无论视口是 320px 还是 1920px，永远是 5 等分。

`min-width: 0` 是关键细节：flex 子项默认 `min-width: auto`（不小于内容宽度），一旦徽章或文字变宽就会把等分撑破。设为 0 才能自由收缩。

### 固定效果怎么做的？

```css
.wx-tabbar { position: fixed; bottom: 0; left: 0; right: 0; }
body       { padding-bottom: calc(62px + env(safe-area-inset-bottom)); }
```

`fixed` 相对视口定位，滚动不移动。但脱离文档流后会盖住页面最后一块内容，所以 `body` 要加等高的 `padding-bottom` 补回来。

`env(safe-area-inset-bottom)` 是 iPhone 全面屏底部小黑条的高度，不加会被遮挡。

### 图标大小和颜色怎么改？

**字体图标方案**——把它当文字处理：

```css
.wx-tabbar__icon {
  font-size: 22px;   /* 改这里 = 改图标大小 */
  color: #8fa698;    /* 改这里 = 改图标颜色 */
}
```

**SVG 方案**——用 `em` + `currentColor`：

```css
.wx-svgtab__icon {
  width: 1.5em;              /* 随 font-size 缩放，矢量不失真 */
  fill: currentColor;        /* 继承父级 color */
}
```

## 六、常见问题

**Q：图标显示成方块 / 空白？**
A：`iconfont` 文件夹路径不对，或 `iconfont.css` 没引入成功。F12 → Network 面板看 `iconfont.woff2` 是否 404。

**Q：图标位置错乱、显示成字母？**
A：类名不匹配。打开 `iconfont/demo_index.html` 对照真实类名。

**Q：下导航盖住页面底部内容？**
A：`body` 的 `padding-bottom` 小了。量一下导航实际高度，改大一点（当前 62px）。

**Q：5 项挤在一起换行了？**
A：检查是否有 `min-width: 0`；另外确认没给 `.wx-tabbar__icon-wrap` 设固定大宽度。

---

本项目为课程实验作品，内容仅供科普学习。野外技能请在有专业指导的情况下练习。
