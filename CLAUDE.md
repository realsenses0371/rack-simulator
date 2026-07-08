# 弱电机柜模拟安装

单文件 Web 应用，拖拽设备到机柜进行模拟安装，导出 PNG 图片。

## 技术栈

- 纯 HTML + CSS + JS，单文件 `index.html`
- HTML5 Drag & Drop API
- html2canvas (CDN) 导出图片
- 无框架、无构建工具、零依赖运行

## 文件结构

```
index.html   — 完整应用（样式 + 逻辑）
README.md    — 项目说明
CLAUDE.md    — 开发指南
```

## 代码结构

| 区域 | 说明 |
|------|------|
| `state` | 全局状态：rackHeight / uHeight / devices[] / nextId |
| `renderRack()` | 渲染机柜，设置 innerHTML 后遍历 devices 添加设备块 |
| `renderDeviceBlock(dev)` | 渲染单个设备块，动态计算字号/按钮大小 |
| `canPlaceDevice(uPos, uSize, excludeId)` | 检查位置是否可用（边界 + 不重叠） |
| `findNearestPos(dev, dir)` | 向上/下搜索最近可用空位（可跨设备） |
| `moveDeviceUp/Down(id)` | 上下移动设备 |
| `updateSlotHighlights()` | 拖拽时高亮 U 槽位 |
| `exportImage()` | html2canvas 导出 PNG |
| `openEditModal(id)` | 打开设备编辑弹窗 |
| `clearSelection()` | 清除手机端设备选中状态 |
| `_selectedSize` / `_dragStarted` | 手机端选中尺寸 / 拖拽标记 |

## 交互

**桌面端：**
- 左侧面板拖拽设备 → 中间机柜区松开放置
- 悬停设备块显示 ▲▼ 箭头和 × 删除按钮
- 点击设备块打开编辑弹窗（名称/颜色/预设）
- 右侧面板：切换机柜高度 / 统计 / 设备列表 / 导出

**手机端（≤768px）：**
- 设备面板变为水平滚动条
- 点击设备卡片选中（高亮） → 点击机柜目标位置放置
- 再次点击已选中卡片或点空白处取消选中
- 设置面板移至底部，布局紧凑

## 部署

GitHub Pages: `realsenses0371.github.io/rack-simulator/`

更新后推送即自动部署：

```
git add index.html && git commit -m "描述改动" && git push
```
