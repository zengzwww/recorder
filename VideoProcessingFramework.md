# VideoProcessingFramework

## FAQ

### Q1: ImportError: /usr/lib/x86_64-linux-gnu/libgobject-2.0.so.0: undefined symbol: ffi_type_uint32, version LIBFFI_BASE_7.0

```bash
Traceback (most recent call last):
  File "/.../anaconda3/envs/.../lib/python3.8/site-packages/PyNvCodec/__init__.py", line 17, in <module>
    from ._PyNvCodec import *  # noqa
ImportError: /usr/lib/x86_64-linux-gnu/libgobject-2.0.so.0: undefined symbol: ffi_type_uint32, version LIBFFI_BASE_7.0

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "test.py", line 3, in <module>
    import PyNvCodec as nvc
  File "/.../anaconda3/envs/.../lib/python3.8/site-packages/PyNvCodec/__init__.py", line 21, in <module>
    raise RuntimeError("Failed to import native module _PyNvCodec! "
RuntimeError: Failed to import native module _PyNvCodec! Please check whether "/.../anaconda3/envs/.../lib/python3.8/site-packages/PyNvCodec/_PyNvCodec.cpython-38-x86_64-linux-gnu.so" exists and can find all library dependencies (CUDA, ffmpeg).
On Unix systems, you can use `ldd` on the file to see whether it can find all dependencies.
On Windows, you can use "dumpbin /dependents" in a Visual Studio command prompt or
https://github.com/lucasg/Dependencies/releases.
```

**A1:**
```bash
export LD_PRELOAD=/usr/lib/x86_64-linux-gnu/libffi.so.7
```
