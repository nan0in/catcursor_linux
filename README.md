# 普通的鼠标指针 (Linux)

Windows 版原作者：**HappyCadogt**
Bilibili: https://space.bilibili.com/406949928

## 来源
原始 Windows 鼠标指针包 V1.4 来自上述作者。
Linux XCursor 兼容版本由 `win2xcur` + `xcursorgen` 转换生成，支持 8~64px 共 12 档尺寸。

## 安装
```bash
cp -r 普通的鼠标指针 ~/.icons/
# 或
cp -r 普通的鼠标指针 ~/.local/share/icons/
```

启用：
```bash
gsettings set org.gnome.desktop.interface cursor-theme "普通的鼠标指针"
# 或在 Hyprland 中：
hyprctl setcursor "普通的鼠标指针" 24
```

## 文件结构
```
普通的鼠标指针/
├── cursor.theme
├── index.theme
└── cursors/
    ├── left_ptr          (普通选择)
    ├── left_ptr_watch    (后台运行)
    ├── wait              (忙碌)
    ├── cross             (精确选择)
    ├── xterm             (文本选择)
    ├── pencil            (手写)
    ├── circle            (不可用)
    ├── bottom_side       (上下拉伸)
    ├── left_side         (左右拉伸)
    ├── bottom_left_corner
    ├── bottom_right_corner
    ├── move              (移动)
    ├── dotbox            (候选)
    ├── hand2             (链接选择)
    ├── question_arrow    (帮助选择)
    └── ... (别名链接)
```
