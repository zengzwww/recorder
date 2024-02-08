# faceswap

## GFPGANFaceAugment

### preprocess

Original:
```bash
        img = img.astype(np.float32) / 255.0
        img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
        if self.need_norm:
            img = (img - np.float32((0.5, 0.5, 0.5))) * (1 / np.float32((0.5, 0.5, 0.5)))
        t_img = np.expand_dims(img.transpose(2, 0, 1), 0).copy()
```

Optimized:
```bash
        if self.img_chw is None:
            self.img_chw = np.zeros((3, img.shape[0], img.shape[1]),
                                    dtype=np.uint8)
        img_vec = [self.img_chw[2, ...],
                   self.img_chw[1, ...],
                   self.img_chw[0, ...]]
        cv2.split(img, mv=img_vec)
        img_chw = self.img_chw.astype(np.float32)
        if self.need_norm:
            img_chw = (img_chw - 127.5) / 127.5
        t_img = np.expand_dims(img_chw, axis=0)
```

### postprocess

Original:
```bash
        output = outputs[0][0].clip(-1, 1)
        output = (output + 1) / 2
        output = output.transpose(1, 2, 0)
        output = cv2.cvtColor(output, cv2.COLOR_RGB2BGR)
        output = (output * 255.0).round()
        output = output.astype(np.uint8)
```

Optimized:
```bash
        img_chw = outputs[0][0]
        np.multiply(img_chw, np.float32(127.5), out=img_chw)
        np.add(img_chw, np.float32(127.5), out=img_chw)
        np.round(img_chw, out=img_chw)
        np.clip(img_chw, a_min=0, a_max=255, out=img_chw)
        img_uint8 = img_chw.astype(np.uint8)
        img_vec = [img_uint8[2, ...],
                   img_uint8[1, ...],
                   img_uint8[0, ...]]
        output = cv2.merge(img_vec)
```
