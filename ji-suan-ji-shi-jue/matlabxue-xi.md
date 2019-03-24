## 将彩色图片转换成亮度图像
```
img = imread( 'hqdefault.jpg' );
gray_pic = rgb2gray(img);
```

## imhist
* 该函数用于获取图像数据的灰度直方图。
* imhist只能统计灰度图像的直方图，而对于RGB图像则需要分别统计每个通道的直方图。
* 具体用法： 
    * imhist( img );直接显示图像img的灰度直方图； 
    * imhist（img，n）显示一个统计n个灰度级信息的直方图； 
    * [counts, x] = imhist( img ) ；
    > 获取直方图信息，x为灰度级向量，是一个一维向量，里面记录着灰度从0-255所有的值，而countsx也是一个一维向量，里面记录着x中对应灰度值出现的个数。当然x也可以在imhist（i，x）中指定，可以通过stem（x，count）画相应直方图。即统计的灰度级有x个。
    
## numel
* 语法格式：
> n = numel（A）；
> n= numel（A，条件）；
返回数组A中元素个数。若是一幅图像，则numel(A)将给出它的像素数。
