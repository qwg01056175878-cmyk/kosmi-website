# KOSMI 独立网站预览

入口：`previews/kosmi-preview.html`。独立分支：`preview/kosmi-design-20261012`。
基于提交 `ea01b5a1b24820153b14b069cac4d847ee96def4`，未修改 `index.html`，未合并 main，未发布。

## 已实现

黑色、奶油白、香槟金与柔和粉色；OEM/ODM 和 KARA CAT 双入口；中韩英切换与语言记忆；五类目录筛选、九个品类方向；产品详情原生弹窗；手机菜单；键盘焦点和减少动态效果支持。无外部字体、脚本或图片依赖，文件可离线运行。

目录为类别骨架，非完整SKU清单；未填认证、产能、MOQ数值、地址或真实联系方式。展示规划不代表已确认生产或供货。邮箱保持 YOUR_EMAIL@example.com，预览中禁用发送。

## 手机查看

优先在 ChatGPT 点击提供的 HTML 文件链接，使用可执行 HTML 的网页预览。如果文件预览器只显示代码或静态页面，则它不能完整运行这个网页；iPhone“文件”快速查看可能不运行 JavaScript。GitHub 的 blob/Raw 页面也不是网页预览地址。

要在 Safari 可靠测试完整交互，可使用电脑本地服务：

1. 电脑取得本分支文件，进入仓库目录。
2. 运行 `python3 -m http.server 8000 --bind 0.0.0.0`。
3. 电脑与手机连接同一个 Wi-Fi，查电脑在此 Wi-Fi 下的局域网 IP。
4. 手机 Safari 打开 `http://电脑局域网IP:8000/previews/kosmi-preview.html`。
5. 查看中、韩、英；打开菜单；测试全部及五个筛选；打开品类详情。
6. 测试完成，在电脑终端按 Ctrl+C 停止服务。

此方式不会发布到 GitHub Pages。没有创建公网预览地址。

## 扩展产品和真实图片

HTML 内 `script#catalog-data` 是可编辑 JSON，当前九个条目。每条使用稳定唯一 `id` 和 category：`makeup`、`base-sun`、`skincare`、`cleansing`、`fragrance`。

字段：kind、visualLabel、image、alt、name、description、status、sku、specifications。name、description、alt 均含 zh/ko/en。当前 kind 为 category、image 为 null；未确认SKU和规格保持 null。字段 sku/specifications 预留，暂不在品类卡展示；后续单品展示时再扩展渲染。

建议真实图片放在：

- assets/images/products/makeup/
- assets/images/products/base-sun/
- assets/images/products/skincare/
- assets/images/products/cleansing/
- assets/images/products/fragrance/
- assets/images/brand/
- assets/images/factory/

命名：`{brand}-{category}-{sku}-{view}-{ratio}-v{n}.webp`。小写英文、数字、连字符，避免中文、空格或百分号。卡片建议 800×600、4:3。例：`kara-cat-lipstick-kc001-front-4x3-v1.webp`。

从预览HTML引用的 image 路径：`../assets/images/products/makeup/kara-cat-lipstick-kc001-front-4x3-v1.webp`。

填真实 image 后，同时更新三语言 alt。图片加载成功自动隐藏占位提示，加载失败仍保留CSS占位。供货说明不会因有图片自动变成确认状态，应根据核实资料编辑。新增单品或类别复制 JSON 条目即可；新增第六个大类需同步修改 categories 数组和三语言 category_ 键。

首屏和品牌区暂用标注过的抽象/文字占位视觉，非照片、非正式Logo文件。正式品牌标识与工厂照片待核实提供。

## 验证结果

通过：JavaScript语法；66个翻译键一致；9个条目与5种分类；唯一ID、页内链接、禁用邮件发送；自建DOM模拟中的三语言切换、筛选结果9/2/2/2/2/1、弹窗开关、菜单开关及非法语言回退。

尚未验证：真实浏览器的排版、触摸和Safari行为。环境无浏览器程序，下载Chromium失败。已编写320/390/768/1440px响应式规则，但不能声称实际视觉检查通过。发布前应完成以上尺寸的实测、键盘导航、刷新语言记忆和真实图片失败回退验证。
