# christmas-tree-v17.6 🎄

视频同款的「赛博粒子圣诞树」：Three.js 粒子树 + MediaPipe 手势识别 + 拍立得照片挂件。
页面为原作者 [electronicminer/gesture-Christmas_tree-3d_with_photo](https://github.com/electronicminer/gesture-Christmas_tree-3d_with_photo) 的开源作品，
本仓库在原版基础上做了这些改动：依赖从 jsdelivr 换到国内可直接访问的 `registry.npmmirror.com`；移除了会阻塞页面加载的第三方统计脚本；
界面控件中文化；新增了访客自助上传照片的模块。

访问地址：https://wlz200319.github.io/christmas-tree-v17.6/

---

## 玩法

**鼠标 / 触屏**

- 按住拖动：旋转视角
- 滚轮 / 双指：缩放
- 点照片：放大聚焦
- 底部三个圆钮：🎄 树形态 / ✨ 炸散成星云 / 🔍 随机聚焦一张照片
- 按 `H`：隐藏所有按钮，方便截图录屏

**手势（需要摄像头）**

1. 点右上角 `📷 启用手势`，浏览器会弹窗请求摄像头权限，选「允许」
2. 首次会下载约 8MB 的 AI 模型，等十几秒
3. 手心对着镜头：
   - ✋ 张开手掌 = 粒子炸散成星云，同时可用手转动视角
   - ✊ 握拳 = 粒子重新聚合成圣诞树
   - 🤏 捏合 = 随机抓一张照片放大给你看

**照片（谁打开这个网页都能传自己的）**

1. 点 `🖼 上传照片`，可以一次选多张；也可以直接把照片文件拖进页面
2. 照片会自动压缩（长边 1400px），变成金框拍立得挂在树周围，最多 12 张
3. 照片存在你这台电脑的浏览器里（localStorage），刷新、关掉再打开都还在；换电脑 / 换浏览器就看不到
4. 点 `🗑 清空照片` 一次性全删掉

注意：访客上传的照片只保存在各自的浏览器里，不会上传到服务器，所以别人打开链接看到的是他自己传的照片，看不到你的。
想让「所有人打开都自带同一批照片」，用下面这种打包方式。

**背景音乐（自己加歌）**

1. 点 `🎵 添加音乐`，选一个 mp3 / m4a / wav 文件，会立刻循环播放
2. 播放中按钮变成 `⏸ 暂停音乐`，再点一下变 `▶ 继续音乐`
3. 直接把音乐文件拖进页面也行
4. 因为浏览器禁止"没点过页面就自动放声音"，如果放不出来，在页面上随便点一下就会开始

**把照片打包进页面（所有人打开都能看到）**

把照片放进仓库 `images/` 目录，命名为 `(1).jpg`、`(2).jpg` …（也支持 png），
再把 `index.html` 里 `CONFIG.preload.scanCount` 改成照片数量，页面启动时会自动挂到树上。

---

## 技术说明

- `index.html` 是唯一页面文件，其余全是外部依赖（npmmirror CDN 直连）
- three.js 0.160 + 后期处理（Bloom 泛光）
- MediaPipe Hand Landmarker 做手势识别
- 照片上传用 Canvas 压缩后转 dataURL 存 localStorage，启动时自动恢复
- 双击本地文件打开也能看到粒子树，但摄像头手势需要 http(s) 环境（浏览器安全策略限制）

## 改文字 / 改风格

| 想改什么 | 位置 |
| --- | --- |
| 大标题 `MERRY CHRISTMAS` | `index.html` 里 `<h1>` |
| 树的粒子数量与形态 | `CONFIG.particles` |
| 金色 / 深绿主色 | `CONFIG.colors` |
| 自动挂载照片数量 | `CONFIG.preload.scanCount` |
| 照片轨道半径 / 大小 | `updatePhotoLayout()` 里的 `R`、`addPhotoToScene()` 里的 `const s` |
| 最多可挂几张照片 | `MAX_PHOTOS` |
| 礼物盒颜色 | `createParticles()` 里的 `giftPalette`、`giftMats` |
| 默认音量 | `startBgm()` 里的 `bgmAudio.volume` |
