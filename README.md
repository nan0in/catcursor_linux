# 普通的鼠标指针

中文 | 适用于 [GNU](https://www.gnu.org/)/[Linux](https://kernel.org/) 平台

## 关于项目

- **原作者**：[哔哩哔哩 @HappyCadogt](https://space.bilibili.com/406949928)
- Linux 移植：本项目

由于截至项目发布，原作者仅为 Windows 平台提供适配，尚未提供 [GNU](https://www.gnu.org/)/[Linux](https://kernel.org/) 版本，遂将其转换为适用于大多数桌面环境的 [XDG 光标主题包](https://specifications.freedesktop.org/icon-theme/latest/)，以供 [GNU](https://www.gnu.org/)/[Linux](https://kernel.org/) 用户使用。**特别感谢原作者 HappyCadogt 的付出和努力。**

## 项目内容

- 由 [**HappyCadogt**](https://space.bilibili.com/406949928) 设计并制作
- 来源版本：**V1.4**（Windows `.ani`/`.cur` 原始文件）
- **全部**为动态图标
- 支持 **8 / 12 / 16 / 20 / 24 / 28 / 32 / 36 / 40 / 48 / 56 / 64** 多分辨率

## 适用平台

- [GNU](https://www.gnu.org/)/[Linux](https://kernel.org/) 平台所有支持 [XDG 光标主题](https://specifications.freedesktop.org/icon-theme/latest/) 的桌面环境
- 已在 [Hyprland](https://hyprland.org/) 通过测试，表现良好

## 安装方式

### 为当前用户安装

```bash
git clone https://github.com/<your-repo>/普通鼠标指针-linux.git
mkdir -p ~/.local/share/icons/
cp -r 普通鼠标指针-linux/普通的鼠标指针 ~/.local/share/icons/
```

**或**直接复制 cursors 目录：

```bash
git clone https://github.com/<your-repo>/普通鼠标指针-linux.git
mkdir -p ~/.icons/
cp -r 普通鼠标指针-linux/普通的鼠标指针 ~/.icons/
```

### 为所有用户安装（需 root）

```bash
sudo mkdir -p /usr/share/icons/
sudo cp -r 普通的鼠标指针 /usr/share/icons/
```

## 应用方式

### Hyprland

```bash
hyprctl setcursor "普通的鼠标指针" 24
```

或在 `~/.config/hypr/hyprland.conf` 中添加：

```conf
exec-once = hyprctl setcursor "普通的鼠标指针" 24
```

### GNOME

```bash
gsettings set org.gnome.desktop.interface cursor-theme "普通的鼠标指针"
gsettings set org.gnome.desktop.interface cursor-size 24
```

### KDE Plasma

导航至 **系统设置 → 外观和样式 → 颜色和主题 → 光标**，选择 "普通的鼠标指针"。

### 其他桌面环境 / 窗口管理器

设置 `XCURSOR_THEME` 环境变量：

```bash
export XCURSOR_THEME="普通的鼠标指针"
export XCURSOR_SIZE=24
```

建议写入 `~/.profile` 或 `~/.xprofile`。

---

## 替换件

原作者在 V1.4 中提供了 **"点击"手势的替换件**，用于替换默认的链接悬停光标（`hand2`）。当默认样式审美疲劳时，可替换为新样式。

### 可用替换件

| 替换件 | 帧数 | 说明 |
|---|---|---|
| `Link（1）.ani` | 94 帧 | 鲶鱼主题点击动画 |
| `Link（2）.ani` | 60 帧 | 备选点击动画 |

### 使用方法（Linux）

1. 使用 `win2xcur` 将替换件转为 XCursor：
   ```bash
   pip install win2xcur
   win2xcur 替换件/点击/Link（1）.ani -o /tmp/replace/
   ```

2. 将生成的 `Link（1）` 重命名为 `hand2`，放入光标主题的 `cursors/` 目录覆盖原文件：
   ```bash
   cp /tmp/replace/Link（1） ~/.local/share/icons/普通的鼠标指针/cursors/hand2
   ```

3. 如需多尺寸支持，使用 `xcursorgen` 重新生成（参考 `build-multi-cursor.py`）。

---

## 文件结构

```
普通的鼠标指针/
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

- **原作者** [**HappyCadogt**](https://space.bilibili.com/406949928)，没有他的付出，就没有这个项目
- `win2xcur` + `xcursorgen`，为多分辨率光标转换提供了便捷的方式
- `xcur2png`，用于光标帧提取与调试
