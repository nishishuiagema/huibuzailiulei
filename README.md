# Travel Notes

这是一个可以直接部署到 GitHub Pages 的极简旅行主页。顶部只显示地点和三张照片，屏幕中间 2/3 是照片导轨区，滚轮在这里横向滑动；鼠标悬停时照片轻微扇形展开，点击旅行后该旅行居中并更大幅度展开，同时在下方生成照片展示页。向下滚动进入展示页后，滚轮继续控制照片横向滑动。

## 部署到 GitHub Pages

1. 在 GitHub 新建仓库：`你的GitHub用户名.github.io`
2. 把本目录里的文件上传到仓库根目录
3. 打开仓库 `Settings` -> `Pages`
4. Source 选择 `Deploy from a branch`
5. Branch 选择 `main` 和 `/root`
6. 保存后等待几分钟

主页地址：

```text
https://你的GitHub用户名.github.io
```

## 以后怎么更新照片

不用改 `index.html`。日常只改两类文件：

- `assets/photos/`: 放旅行照片
- `data/trips.json`: 写旅行记录

在 GitHub 网页端也能更新：

1. 打开仓库里的 `assets/photos`
2. 点击 `Add file` -> `Upload files`
3. 上传新照片，例如 `hangzhou.jpg`
4. Commit changes
5. 打开 `data/trips.json`
6. 点击铅笔图标编辑
7. 在 `trips` 数组里新增一条记录
8. Commit changes

新增记录示例：

```json
{
  "id": "hangzhou-2026",
  "place": "杭州",
  "images": [
    "assets/photos/hangzhou-1.jpg",
    "assets/photos/hangzhou-2.jpg",
    "assets/photos/hangzhou-3.jpg"
  ],
  "photos": [
    {
      "src": "assets/photos/hangzhou-1.jpg",
      "time": "2026.07.07",
      "text": "西湖边走了一下午。"
    },
    {
      "src": "assets/photos/hangzhou-2.jpg",
      "time": "2026.07.08",
      "text": "早上去了灵隐寺。"
    },
    {
      "src": "assets/photos/hangzhou-3.jpg",
      "time": "2026.07.08",
      "text": "傍晚在龙井村停了一会。"
    }
  ]
}
```

字段说明：

- `place`: 顶部显示的地点
- `images`: 顶部三张重叠照片
- `photos`: 点击旅行后展示区里的照片卡片
- `time`: 该照片的时间
- `text`: 该照片的说明

## 什么时候需要改 HTML

只在你想改版式、颜色、字体、交互时改 `index.html`。新增旅行地点、替换照片、改时间和说明，都只需要改 `data/trips.json`。

## 这里用到的前端术语

- 每次旅行：可以叫 `trip entry`、`travel stop`、`timeline item`，中文叫“旅行条目”或“时间轴节点”。
- 三张重叠照片：可以叫 `photo stack` 或 `image stack`，中文叫“照片堆叠”。
- 中间可横滑区域：可以叫 `rail zone`，中文叫“导轨区”。
- 鼠标悬停后展开：可以叫 `fan-out interaction`，中文叫“扇形展开”。
- 点击后选中的旅行：可以叫 `selected trip`，中文叫“选中旅行”。
- 白底上的模糊大图背景：可以叫 `ambient background`，中文叫“氛围背景”。

## 关于数据库和服务器

GitHub Pages 是静态托管，不需要服务器和数据库。

如果想在网页上点按钮后直接保存到线上，需要额外后端，例如 GitHub API + serverless 函数、Supabase、Firebase 或 Cloudflare Workers。不要把 GitHub Token 写进前端 JavaScript。
