# PyAV

## Installation

* Install ffmpeg

```bash
sudo apt install ffmpeg
sudo apt install libavformat-dev
sudo apt install libavcodec-dev
sudo apt install libavdevice-dev
sudo apt install libavutil-dev
sudo apt install libavfilter-dev
sudo apt install libswscale-dev
sudo apt install libswresample-dev
```

Configure env PKG_CONFIG_PATH

```bash
export PKG_CONFIG_PATH=/usr/lib/x86_64-linux-gnu/pkgconfig:$c
```

libavcodec.pc, etc. in /usr/lib/x86_64-linux-gnu/pkgconfig directory.

* Install PyAV

```bash
echo "cython<3.0" >> c.txt
PIP_CONSTRAINT=c.txt pip install av --no-binary av
```

See:
[here](https://stackoverflow.com/questions/72604912/cant-show-image-with-opencv-when-importing-av) and [there](https://github.com/PyAV-Org/PyAV/issues/1140#issuecomment-1642460904)
