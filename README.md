<div align="center">

<img src="https://free.picui.cn/free/2025/08/11/6899bb5b91222.png" alt="logo" width="200" height="200">

# AntiCAP

<strong>Version:3.1.6</strong>


| 类型         | 状态 | 描述                                    |
|------------|-|---------------------------------------|
| `OCR识别`    |✅| 返回图片字符串                               |
| `数学计算`     |✅| 返回计算结果                                |
| `缺口滑块`     |✅| 返回坐标                                  |
| `阴影滑块`     |✅| 返回坐标                                  |
| `图标点选`     |✅| 侦测图标位置 或 按序返回坐标                       |
| `文字点选`     |✅| 侦测文字位置 或 按序返回坐标                       |
| `相似对比`     |✅| 图片中文字的相似度对比                           |
| `WebApi服务` | ✅ | https://github.com/81NewArk/AntiCAP-WebApi |


</div>

## 免责声明

本项目仅用于学习和研究目的，严禁将其用于任何违反中华人民共和国法律法规、第三方服务条款或社会伦理的行为。开发者不对因本项目的使用、传播或修改所产生的任何直接或间接后果承担责任。

使用本项目即表示您理解并自动遵守以下条款：

1. **合法使用**：不得将本项目用于恶意攻击、网络诈骗、绕过身份验证、未经授权的数据抓取、验证码识别滥用等非法用途。

2. **风险自负**：您自愿承担使用本项目所带来的一切法律和技术风险，包括但不限于服务封禁、数据丢失、法律纠纷等。

3. **开发者免责**：项目作者对任何因使用本项目而引发的损失、损害、违法行为或法律责任不承担任何形式的赔偿或担保义务。

4. **禁止商业化滥用**：不得将本项目用于违法牟利，包括但不限于变相收费、集成进商业软件、参与“黑产”活动等。

---
**若您不同意上述条款，请立即停止使用并删除本项目。**




<br>

<div align="center">

# 📄 AntiCAP 文档

</div>

## 🌍环境说明

```
python >=3.8  64bit
```

## 📁 安装


###  Pypi下载
```
pip install AntiCAP -i https://pypi.tuna.tsinghua.edu.cn/simple
```
<div align="center">

## 🤖 调用说明

</div>

###  1. 通用OCR识别
#### 参考例图 (数字、大小写字母、汉字)
<img src="https://free.picui.cn/free/2025/07/30/68896c92e18f0.jpg">


```python
# example.py

import base64
import AntiCAP


with open("captcha.jpg", "rb") as img_file:
    img_base64 = base64.b64encode(img_file.read()).decode('utf-8')


Atc = AntiCAP.Handler(show_banner=True)
result = Atc.OCR(img_base64=img_base64) #传入图片Base64编码字符串

print(result) # 返回字符串 jepy
```

---



###  2. 算术验证码识别
#### 参考例图 (加减乘除类) 目前模型泛化能力较弱 等待更新
<img src="https://free.picui.cn/free/2025/07/30/6889718adee8f.jpg">


```python
# example.py

import base64
import AntiCAP


with open("captcha.jpg", "rb") as img_file:
    img_base64 = base64.b64encode(img_file.read()).decode('utf-8')


Atc = AntiCAP.Handler(show_banner=True)
result = Atc.Math(img_base64=img_base64) #传入图片Base64编码字符串

print(result) #返回计算结果 8

```


---



###  3. 图标侦测
#### 参考例图
<img src="https://free.picui.cn/free/2025/07/30/688972d69d3c1.jpg" width="200" height="200">


```python
# example.py

import base64
import AntiCAP


with open("captcha.jpg", "rb") as img_file:
    img_base64 = base64.b64encode(img_file.read()).decode('utf-8')


Atc = AntiCAP.Handler(show_banner=True)
result = Atc.Detection_Icon(img_base64=img_base64) #传入图片Base64编码字符串

print(result)

# [{'class': 'icon', 'box': [9.12, 105.4, 111.73, 223.02]}...]
# box分别为 [x1, y1, x2, y2] 左上角和右下角坐标

```


---



###  4. 文字侦测
#### 参考例图
<img src="https://free.picui.cn/free/2025/07/30/688974085b38e.jpg" width="200" height="200">


```python
# example.py

import base64
import AntiCAP


with open("captcha.jpg", "rb") as img_file:
    img_base64 = base64.b64encode(img_file.read()).decode('utf-8')


Atc = AntiCAP.Handler(show_banner=True)
result = Atc.Detection_Text(img_base64=img_base64) #传入图片Base64编码字符串

print(result)
# [{'class': 'Text', 'box': [145.71, 19.21, 223.99, 95.7]}...]
# box分别为 [x1, y1, x2, y2] 左上角和右下角坐标
```


---




###  5. 图标点选类
#### 提示图
<img src="https://free.picui.cn/free/2025/07/30/688975c92514c.jpg" width="200" height="50">

#### 目标图片
<img src="https://free.picui.cn/free/2025/07/30/688972d69d3c1.jpg" width="200" height="200">


```python
# example.py

import base64
import AntiCAP

with open("order_image.jpg", "rb") as f:
    order_img_base64 = base64.b64encode(f.read()).decode('utf-8')

# 读取目标图（所有图标）并转为 base64
with open("target_image.jpg", "rb") as f:
    target_img_base64 = base64.b64encode(f.read()).decode('utf-8')

Atc = AntiCAP.Handler(show_banner=True)
result = Atc.ClickIcon_Order(
    order_img_base64=order_img_base64,
    target_img_base64=target_img_base64
)

print(result)
```



---



###  6. 文字点选类
#### 提示图
<img src="https://free.picui.cn/free/2025/07/30/6889773219292.jpg" width="200" height="50">

#### 目标图片
<img src="https://free.picui.cn/free/2025/07/30/688974085b38e.jpg" width="200" height="200">


```python
# example.py

import base64
import AntiCAP

with open("order_image.jpg", "rb") as f:
    order_img_base64 = base64.b64encode(f.read()).decode('utf-8')

# 读取目标图（所有图标）并转为 base64
with open("target_image.jpg", "rb") as f:
    target_img_base64 = base64.b64encode(f.read()).decode('utf-8')

Atc = AntiCAP.Handler(show_banner=True)
result = Atc.ClickIcon_Order(
    order_img_base64=order_img_base64,
    target_img_base64=target_img_base64
)

print(result)
```



---



###  7. 缺口滑块类
#### 缺口图
<img src="https://free.picui.cn/free/2025/07/30/68897881c804c.png" width="50" height="120">

#### 背景图
<img src="https://free.picui.cn/free/2025/07/30/688978834962d.jpg" width="400" height="200">

```python
# example.py

import base64
import AntiCAP

# 读取滑块图片（小块）
with open("slider.png", "rb") as f:
    target_base64 = base64.b64encode(f.read()).decode('utf-8')

# 读取背景图片（带缺口的大图）
with open("background.jpg", "rb") as f:
    background_base64 = base64.b64encode(f.read()).decode('utf-8')


Atc = AntiCAP.Handler(show_banner=True)

result = Atc.Slider_Match(target_base64=target_base64,
                          background_base64=background_base64
)

print(result)
```



---




###  8. 阴影滑块类
#### 目标图片
<img src="https://free.picui.cn/free/2025/07/30/68897997591b9.jpg" width="400" height="200">

#### 背景图片
<img src="https://free.picui.cn/free/2025/07/30/68897997a65d7.jpg" width="400" height="200">

```python
# example.py

import base64
import AntiCAP

# 读取滑块图片（小块）
with open("target.jpg", "rb") as f:
    target_base64 = base64.b64encode(f.read()).decode('utf-8')

# 读取背景图片（带缺口的大图）
with open("background.jpg", "rb") as f:
    background_base64 = base64.b64encode(f.read()).decode('utf-8')


Atc = AntiCAP.Handler(show_banner=True)

result = Atc.Slider_Match(target_base64=target_base64,
                          background_base64=background_base64
)

print(result)
```



---




###  9. 相似度对比
#### 图片1
<img src="https://free.picui.cn/free/2025/07/30/68897a1a09ecc.jpg" width="100" height="100">

#### 图片2
<img src="https://free.picui.cn/free/2025/07/30/68897a1a0b5b7.jpg" width="100" height="100">

```python
# example.py
import base64
import AntiCAP

with open("image1.jpg", "rb") as f:
    image1_base64 = base64.b64encode(f.read()).decode('utf-8')

with open("image2.jpg", "rb") as f:
    image2_base64 = base64.b64encode(f.read()).decode('utf-8')


Atc = AntiCAP.Handler(show_banner=True)

result = Atc.compare_image_similarity(image1_base64=image1_base64, image2_base64=image2_base64)

print("相似度结果:", result)

```


---



<div align="center">

<img src="https://free.picui.cn/free/2025/07/04/6867efd0bd67e.png" alt="Ali" width="200" height="200">
<img src="https://free.picui.cn/free/2025/07/04/6867efd0d7cbb.png" alt="Wx" width="200" height="200">

</div>

<br>

# 💪🏼 模型训练

<br>

<div align="center">

<img src="https://free.picui.cn/free/2025/07/04/6867f0684ff6e.png" width="200" height="200">

<strong>https://github.com/81NewArk/AntiCAP_trainer</strong>

根据自身要求训练模型 无缝衔接下一个 下一个更乖。

</div>

