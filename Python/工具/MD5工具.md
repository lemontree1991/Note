```python
import hashlib

def md5sum(filename, chuck=51200):
    # hash_ = hashlib.sha256()
    hash_ = hashlib.md5() # 造出hash工厂
    with open(filename, "rb") as f:
        # 必须是rb形式打开的，否则的两次出来的结果不一致
        for block in iter(lambda: f.read(chuck), b""):
            hash_.update(block)
    return hash_.hexdigest() # 产出hash值
```

