## mp4 to 264

```bash
ffmpeg -i test.mp4 -c h264 test.264
```
## 录屏

```bash
ffmpeg -video_size 1920x1080 -framerate 25 -f x11grab -i :0.0+0,0 output.mp4
```

[参考](https://trac.ffmpeg.org/wiki/Capture/Desktop)

## 设置旋转元数据

[这种方法不用对视频重新编码](https://creatomate.com/blog/how-to-rotate-videos-using-ffmpeg)

顺时针旋转90度
```bash
ffmpeg -i /home/dlyrm/Downloads/gold-rush.mp4 -metadata:s:v rotate="-90" -codec copy /home/dlyrm/Downloads/gold-rush_90.mp4
```

顺时针旋转180度
```bash
ffmpeg -i /home/dlyrm/Downloads/gold-rush.mp4 -metadata:s:v rotate="-180" -codec copy /home/dlyrm/Downloads/gold-rush_180.mp4
```

逆时针旋转90度(顺时针旋转270度)
```bash
ffmpeg -i /home/dlyrm/Downloads/gold-rush.mp4 -metadata:s:v rotate="90" -codec copy /home/dlyrm/Downloads/gold-rush_270.mp4
```

用ffprobe检测旋转元数据, 显示90, 不是-90
```bash
ffprobe -loglevel error -select_streams v:0 -show_entries stream_tags=rotate -of default=nw=1:nk=1 -i /home/dlyrm/Downloads/gold-rush_clockwise.mp4
```

用ffprobe检测旋转元数据, 显示270, 不是90
```bash
ffprobe -loglevel error -select_streams v:0 -show_entries stream_tags=rotate -of default=nw=1:nk=1 -i /home/dlyrm/Downloads/gold-rush_counterclockwise.mp4
```

下面的方法更慢, 会分别显示-90和90
```bash
ffprobe -loglevel error -select_streams v:0 -show_entries side_data="rotation" -of default=nw=1:nk=1 -i /home/dlyrm/Downloads/gold-rush_clockwise.mp4
ffprobe -loglevel error -select_streams v:0 -show_entries side_data="rotation" -of default=nw=1:nk=1 -i /home/dlyrm/Downloads/gold-rush_counterclockwise.mp4
```
