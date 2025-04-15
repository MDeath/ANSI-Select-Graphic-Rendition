# ANSI-Select-Graphic-Rendition
为 ANSI 提供图形格式支持 SGR(Select Graphic Rendition)

```python
def SGR(text:str,setup:str='',b4:int=None,B4:int=None,b8:int=None,B8:int=None,r:int=None,g:int=None,b:int=None,R:int=None,G:int=None,B:int=None) -> str:
    '''# Select Graphic Rendition 
    text 文本
    - setup 字体设置组合
        - b 加粗或增亮
        - l 增暗
        - i 斜体
        - u 下划线
        - uu 双下划线
        - d 删除线
        - t 上划线
        - f 闪烁
        - r 反转字色和底色
        - h 隐藏
    - b4 4-bit 字色 | B4 4-bit 底色: 0-7 增亮 10-17
    - b8 8-bit 字色 | B8 8-bit 底色: 0-255
    - r,g,b RGB字色 | R,G,G RGB底色'''
    conf = []
    if 'b'in setup.lower():conf.append('1') # 加粗或增亮
    if 'l'in setup.lower():conf.append('2') # 增暗
    if 'i'in setup.lower():conf.append('3') # 斜体
    if 'u'in setup.lower():conf.append('4') # 下划线
    if 'uu'in setup.lower():conf.append('21') # 双下划线
    if 'd'in setup.lower():conf.append('9') # 删除线
    if 't'in setup.lower():conf.append('53') # 上划线
    if 'f'in setup.lower():conf.append('5') # 闪烁
    if 'r'in setup.lower():conf.append('7') # 反显
    if 'h'in setup.lower():conf.append('8') # 隐藏
    if b4 in range(0,8) or b4 in range(10,18):conf.append(str(b4+30 if b4 < 9 else b4+80)) # 0-7 之间 黑、红、绿、黄、蓝、紫、青、白 10-17 增亮
    if B4 in range(0,8) or B4 in range(10,18):conf.append(str(B4+40 if B4 < 9 else B4+90)) # 0-7 之间 黑、红、绿、黄、蓝、紫、青、白 10-17 增亮
    if b8 in range(256):conf += ['38','5',str(b8)] # 0-255 之间 8-bit 色彩
    if B8 in range(256):conf += ['48','5',str(B8)] # 0-255 之间 8-bit 色彩
    if any([i in range(256) for i in [r,g,b]]):conf += ['38','2',str(r or 0),str(g or 0),str(b or 0)]
    if any([i in range(256) for i in [R,G,B]]):conf += ['48','2',str(R or 0),str(G or 0),str(B or 0)]
    return f'\033[{";".join(conf)}m{text}\033[0m
```
