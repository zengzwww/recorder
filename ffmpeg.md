## mp4 to 264

```bash
ffmpeg -i test.mp4 -c h264 test.264
```
## 录屏

```bash
ffmpeg -video_size 1920x1080 -framerate 25 -f x11grab -i :0.0+0,0 output.mp4
```

[参考](https://trac.ffmpeg.org/wiki/Capture/Desktop)
