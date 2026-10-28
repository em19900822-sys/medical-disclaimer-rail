# HOWTO · 医疗说明条

在用户 Windows 电脑上对 1080×1920 竖屏视频叠免责说明。

## 工作目录

在输出旁建工作目录（例如 `医疗说明条/`），放入：

1. `text.txt`（UTF-8，两行文案）
2. `vf.txt`：

```
drawtext=fontfile=C\:/Windows/Fonts/msyhbd.ttc:textfile=text.txt:fontcolor=white@0.5:fontsize=28:line_spacing=6:shadowcolor=black@0.12:shadowx=1:shadowy=1:x=(w-text_w)/2:y=h-25-text_h
```

## 预览一帧

```powershell
ffmpeg -y -i frame.png -filter_complex_script vf.txt -update 1 sample.png
```

## 整片

```powershell
Set-Location -LiteralPath <工作目录>
ffmpeg -y -i <输入.mp4> -filter_complex_script vf.txt -map 0:a? -c:v libx264 -preset medium -crf 18 -c:a copy out.mp4
```

中文路径不要塞进 `drawtext` 参数；先 `Set-Location`，用相对 `text.txt`。
