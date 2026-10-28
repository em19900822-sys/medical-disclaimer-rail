---
name: 医疗说明条
description: 给口播竖屏视频叠底部半透明医疗免责说明小字。用户说「加医疗说明条」「叠免责声明」或丢来视频路径要叠说明时用。
---
# 医疗说明条

给已粗剪/已加章节导航的竖屏口播视频，在画面底部居中叠一条半透明免责说明小字，风格对齐抖音账号「青姐聊多囊备孕」成片里的说明条。

## 默认文案（两行）

```
本视频为健康科普与个人经验分享，不构成医疗诊断，
备孕问题请咨询专业医生。
```

用户当场给了新文案则用新文案；若明确改默认，更新记忆后再用。

## 样式规格（1080×1920）

- 字体：微软雅黑 Bold（`C:/Windows/Fonts/msyhbd.ttc`）
- 字号：28
- 颜色：`white@0.5`（半透明，不要过硬）
- 行距：`line_spacing=6`
- 轻阴影：`shadowcolor=black@0.12:shadowx=1:shadowy=1`
- 位置：水平居中，`y=h-25-text_h`（贴底，无底框）
- 全程叠加，无动画

## 步骤

1. 确认输入视频路径（用户指定，或同目录最新粗剪/章节导航成片）。
2. 在输出旁工作目录写 `text.txt`（UTF-8，两行文案）和 `vf.txt`（避免中文路径进 filter 参数）：

```
drawtext=fontfile=C\:/Windows/Fonts/msyhbd.ttc:textfile=text.txt:fontcolor=white@0.5:fontsize=28:line_spacing=6:shadowcolor=black@0.12:shadowx=1:shadowy=1:x=(w-text_w)/2:y=h-25-text_h
```

3. 先截一帧做 `sample.png` 给用户过目（用户说「可以了」或明确跳过预览才出整片）。
4. 在含 `text.txt`/`vf.txt` 的目录执行 ffmpeg，用 `-filter_complex_script vf.txt`，视频 `libx264 -preset medium -crf 18`，音频 `-c:a copy`。
5. 成片默认存到用户指定目录；未指定则与输入同目录，文件名加 `-医疗说明条`。
6. 告诉用户完整输出路径。

## 注意

- 在用户电脑上跑（带 machineId），不要拷大视频到 box。
- 中文路径：先 `Set-Location` 到工作目录，filter 里用相对 `text.txt`，不要把带中文的绝对路径塞进 drawtext。
- 不要改成黑底条；原成片是无底框的半透明小字。
