# christmas-tree-v17.6

一个零依赖的单文件网页圣诞树：旋转 3D 粒子树 + 螺旋彩灯 + 飘雪 + 星顶光晕 + 圣诞倒计时。

打开 `index.html` 即可查看，无需安装任何依赖、不联网、无外链资源。

## 页面内容

- **Canvas 粒子树**：1700 个绿色点云组成圆锥树体，按深度排序绘制，有立体体积感
- **螺旋彩灯**：270 颗灯沿着 9 圈螺旋线盘绕，逐颗独立相位闪烁，叠加发光混合模式
- **挂饰与星顶**：16 颗彩色挂饰球，树顶四角星带脉动光晕与缓慢呼吸旋转
- **飘雪与地面光**：远景/近景双层雪，树根处有一圈雪地反光
- **交互**：鼠标/手指按住左右拖动旋转，松手带惯性回正；右上角按钮或双击暂停
- **倒计时**：底部自动计算距离下一个 12 月 25 日还有多少天
- **自适应**：按设备像素比渲染、窗口缩放自动重排，手机端同样可用

## 本地预览

直接双击 `index.html`，或在该目录执行：

```bash
python3 -m http.server 8000
```

然后访问 http://localhost:8000

## GitHub Pages 部署（三条命令版）

```bash
git init
git add .
git commit -m "christmas-tree-v17.6"
git branch -M main
git remote add origin https://github.com/<你的用户名>/christmas-tree-v17.6.git
git push -u origin main
```

推上去后在仓库 **Settings → Pages** 里把 Source 选成 `Deploy from a branch`，分支选 `main`、目录选 `/ (root)`，保存后等 1 分钟左右，访问：

```
https://<你的用户名>.github.io/christmas-tree-v17.6/
```

`.nojekyll` 文件已放好，避免 Pages 用 Jekyll 处理静态文件。

## 自定义

| 想改什么 | 改哪里 |
| --- | --- |
| 树的高矮胖瘦 | `TREE_H`、`TREE_R` |
| 灯的数量/圈数 | `LIGHTS`、`tt * TAU * 9` 里的 `9` |
| 灯的颜色 | `LIGHT_COLORS` 数组 |
| 旋转速度 | `BASE_SPIN`（单位：弧度/秒） |
| 雪的大小 | `newFlake()` 里的 `r`、`vy` |
| 标题文字 | `<h1>` 与 `<p id="count">` |
