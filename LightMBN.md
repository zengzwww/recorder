# LightMBN

## TypeError

Report error:
```bash
Traceback (most recent call last):
  File "main.py", line 20, in <module>
    config = yaml.load(f)
TypeError: load() missing 1 required positional argument: 'Loader'
```

Solution:
Modify LightMBN/main.py:20 as 
```text
config = yaml.load(f, Loader=yaml.Loader)
```

## No module named 'gdown'

```bash
pip install gdown
```
