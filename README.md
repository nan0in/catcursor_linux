# 猫标

中文 | [English](./README_en-US.md)

适用于 [GNU](https://www.gnu.org/)/[Linux](https://kernel.org/) 平台

## 关于项目

- **原作者**：[哔哩哔哩 @HappyCadogt](https://space.bilibili.com/406949928)
- **移植者**：[@Tseshongfeeshur（Ryan）](https://github.com/Tseshongfeeshur)（初始 Linux 移植）、本项目（V1.4 更新 + 多分辨率构建）

本项目基于 Ryan 的 [cat-cursors](https://github.com/Tseshongfeeshur/cat-cursors) 初始移植，同步原作者 V1.4 更新，并增加了 8~64px 共 12 档分辨率支持。

## 项目内容

- 由 [**HappyCadogt**](https://space.bilibili.com/406949928) 设计并制作
- 来源版本：**V1.4**（Windows `.ani`/`.cur` 原始文件）
- **全部**为动态图标
- 支持 **8 / 12 / 16 / 20 / 24 / 28 / 32 / 36 / 40 / 48 / 56 / 64** 多分辨率

## 适用平台

- [GNU](https://www.gnu.org/)/[Linux](https://kernel.org/) 平台所有支持 [XDG 光标主题](https://specifications.freedesktop.org/icon-theme/latest/) 的桌面环境
- 已在 [Hyprland](https://hyprland.org/) 与 KDE Plasma 等多桌面环境通过测试，表现良好

## 安装方式

### 为当前用户安装

```bash
git clone https://github.com/<your-repo>/catcursor_linux.git
mkdir -p ~/.local/share/icons/
cp -r catcursor_linux/猫标 ~/.local/share/icons/
```

**或**直接复制 cursors 目录：

```bash
git clone https://github.com/<your-repo>/catcursor_linux.git
mkdir -p ~/.icons/
cp -r catcursor_linux/猫标 ~/.icons/
```

### 为所有用户安装（需 root）

```bash
sudo mkdir -p /usr/share/icons/
sudo cp -r 猫标 /usr/share/icons/
```

## 应用方式

### Hyprland

```bash
hyprctl setcursor "猫标" 24
```

或在 `~/.config/hypr/hyprland.conf` 中添加：

```conf
exec-once = hyprctl setcursor "猫标" 24
```

### GNOME

```bash
gsettings set org.gnome.desktop.interface cursor-theme "猫标"
gsettings set org.gnome.desktop.interface cursor-size 24
```

### KDE Plasma

导航至 **系统设置 → 外观和样式 → 颜色和主题 → 光标**，选择 "猫标"。

### 其他桌面环境 / 窗口管理器

设置 `XCURSOR_THEME` 环境变量：

```bash
export XCURSOR_THEME="猫标"
export XCURSOR_SIZE=24
```

建议写入 `~/.profile` 或 `~/.xprofile`。

也可通过 DMS 等配置工具进行设置。
---

## 替换件

原作者在 V1.4 中提供了 **"点击"手势的替换件**，用于替换默认的链接悬停光标（`hand2`）。当默认样式审美疲劳时，可替换为新样式。

### 可用替换件

| 替换件 | 帧数 | 说明 |
|---|---|---|
| `Link（1）.ani` | 94 帧 | 鲶鱼主题点击动画 |
| `Link（2）.ani` | 60 帧 | 备选点击动画（当前默认） |

替换件源文件位于仓库 `替换件/` 目录。

### 使用方法（Linux）

安装依赖：
```bash
pip install win2xcur Pillow
# 系统包（Arch）：sudo pacman -S xcur2png xcursorgen
```

以 Link（1）鲶鱼版为例：

```bash
# 1. 将 .ani 转为 XCursor
win2xcur 替换件/Link（1）.ani -o /tmp/replace/

# 2. 提取帧并重建 12 尺寸（8~64px）
python3 build-multi-cursor.py --single /tmp/replace/Link（1） --output hand2

# 3. 覆盖主题中的 hand2
cp hand2 ~/.local/share/icons/猫标/cursors/hand2

# 4. 重新加载
hyprctl setcursor "猫标" 24
```

切换回默认 Link（2）：
```bash
git checkout 猫标/cursors/hand2
hyprctl setcursor "猫标" 24
```

---

## 自行构建

如需从 Windows 源文件（`.ani`/`.cur`）自行构建 Linux 版：

```bash
pip install win2xcur Pillow
```

转换流程见 `build-multi-cursor.py`，核心步骤：

1. `win2xcur` 将 `.ani`/`.cur` 转为单尺寸 XCursor
2. `xcur2png` 提取帧
3. PIL 缩放至目标尺寸
4. `xcursorgen` 生成多尺寸 XCursor
5. 创建别名链接 + `cursor.theme` / `index.theme`

源工程文件位于 `工程文件/`，含各光标类型的 PNG 源帧，可用于二次创作。

---

## 文件结构

```
猫标/
├── cursor.theme
├── index.theme
└── cursors/
    ├── left_ptr          # 普通选择
    ├── left_ptr_watch    # 后台运行
    ├── wait              # 忙碌
    ├── cross             # 精确选择
    ├── xterm             # 文本选择
    ├── pencil            # 手写
    ├── circle            # 不可用
    ├── hand2             # 链接选择
    ├── question_arrow    # 帮助选择
    ├── bottom_side       # 上下拉伸
    ├── left_side         # 左右拉伸
    ├── bottom_left_corner
    ├── bottom_right_corner
    ├── move              # 移动
    ├── dotbox            # 候选
    └── right_ptr / ...   # 别名链接
```

## 鸣谢

- **原作者** [**HappyCadogt**](https://space.bilibili.com/406949928)
- `win2xcur` + `xcursorgen`，为多分辨率光标转换提供了便捷的方式
- `xcur2png`，用于光标帧提取与调试
