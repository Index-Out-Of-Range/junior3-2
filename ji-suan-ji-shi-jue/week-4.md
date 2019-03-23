## 自适应直方图均衡\(AHE\)和限制对比度的自适应直方图均衡\(CLAHE\)

---

### 自适应的直方图均衡\(Adaptive Histogram Equalization\)

#### 算法简介

> AHE是一种用来改善图像对比度的图像处理技术，与传统的直方图均衡相比，不同点主要在于：AHE通过计算图像每一个显著区域的直方图来重新分布图像的亮度值。因此它更适合于用来改善图像的局部对比度，以增强图像边缘信息，利于分割。
>
> 但是，AHE有一个缺陷：在增强对比度的同时也会增强图像同质（均匀）区域的噪声。作为AHE的改进，CLAHE可以有效降低这种噪声的增强

#### 算法的意义

> 传统的直方图均衡对于包含明显较亮或较暗区域的图像来说，不能起到显著的增强效果。
>
> AHE通过计算每一个像素邻域的变换函数来对每个像素执行直方图增强。最简单的形式是，基于该像素的方形区域的直方图来均衡化每一个像素，如下图，这种基于直方图进行增强的思想其实跟普通的直方图增强完全相同，因为这种变换函数与像素邻域的累积分布函数（CDF）是相称的。

![](/images/2019年3月15日21点01分.png)

> 对于图像的边界像素应该特殊处理，因为这些像素的邻域并不完全包含在图像内，比如上图中蓝色框，这可以通过像素行或列的镜像来解决；直接对边界像素行进行复制是不可取的，因为这样会造成像素邻域直方图出现很高的峰值。

#### 算法的性质

> 邻域的size是一个邻域长度的尺度参数，当这个参数较大时，会降低对比度；反之增强对比度；
>
> 由于直方图增强的性质，AHE中的像素变换结果是跟其在邻域像素中的顺序排列成正比的，因此我们可以利用专门的硬件来实现这种邻域中心像素和其他像素之间的比较；一种非归一化的计算方法，可以通过对每一个像素加上一个比中心像素小的值来获得，或者在每一个像素上加上一个邻域像素均值。
>
> 如果一个像素邻域是同质的或均匀的，则该邻域的直方图可能会尖状化，即出现很高的峰值，这时变换函数就会把一个很窄的像素值范围映射到变换结果的整个像素值范围，这也正是上面提到的AHE为什么会增强均匀像素邻域噪声的原因所在。



### 限制对比度的自适应直方图增强\(Contrast Limited AHE\)

#### 基本原理

> CLAHE与AHE最大的不同在于前者对对比度进行了限制，这一特性也可以被应用到全局的直方图均衡中。但实际中它很少被用到。CLAHE中，每一个像素邻域都要进行对比度限制，从而得到对应的变换函数，被用来降低AHE中噪声的增强，
>
> 这主要是通过限制AHE中的对比度增强来实现的。像素周围邻域噪声的增强主要是由变换函数的斜率造成的，由于像素邻域的噪声与邻域的CDF成正比，因此也与邻域直方图在该中心像素位置的值成正比，CLAHE之所以能够限制对比度，是因为它在计算邻域的CDF之前在指定阈值处对直方图进行了修剪，如下图所示，这一做法不仅限制了CDF的斜率，也限制了变换函数的斜率，其中对直方图进行切割所使用的阈值，被称作修剪限制度（clip limit），这个参数不仅依赖于直方图的归一化，而且依赖于像素邻域的size大小，通常设为3到4之间。

![](/images/2019年3月15日21点35分.png)

> 上图中，并没有将修剪掉的那部分直方图直接扔掉，而是采用了更妥当的办法，就是将这些被修剪掉的部分重新均匀的分布到直方图中，从而生成新的直方图。
>
> 另外，在这种重新分布下，有可能导致部分区域会再次超过clip limit，如上图右边的图中标记为绿色的那部分区域，这时我们需要调大clip limit以达到实际需要，如果仍然不能让你满意，可以尝试使用递归的过程来重复这一重新分布直方图的步骤，直到超出的部分对我们的结果影响可以忽略不计。

#### 插值加速

> 上面提到的自适应的直方图均衡算法，不论有没有对对比度进行限制，都需要对每一个像素的像素邻域计算邻域直方图和对应的变换函数，这个过程是相当耗时的。
>
> 因此，在保证算法效果的基础上，插值算法被用来提升计算效率，具体做法如下：
>
> -将图像分为相同size的矩形tile，如下图右，通常分为8x8，即64个tiles；
>
> -分别计算每一个tile的直方图、CDF以及变换函数；对于tiles的中心像素（下图左侧的黑色矩形块），由于满足于上述求得的变换函数，因此可以直接使用所在tile的变换函数得到，而其他像素则需要通过与其最邻近的至少四个像素所在的tiles（即四邻域，还可以8邻域）的变换函数进行插值得到。其中，下图左中蓝色区域标记的像素点是用双线性插值得到（注，这部分像素点占一幅图像的大部分）；边界部分的像素点（绿色标记的区域）是用线性插值得到的；而靠近图像角点部分（红色标记）的像素点则是[通过角](https://www.baidu.com/s?wd=%E9%80%9A%E8%BF%87%E8%A7%92&tn=24004469_oem_dg&rsv_dl=gh_pl_sl_csd)点所在tile的变换函数得到。

![](/images/2019年3月15日22点06分.png)

> 其中插值系数反映了距离最近的tiles的中心像素之间的位置，因此这个插值过程是连续的，因为插值得到的像素点可以近似作中心像素点。
>
> 这一过程虽然增加了线性插值的计算量，但是却大大降低了变换函数的计算次数，所以提高了计算速度。

**参考：**[**https://blog.csdn.net/eternity1118\_/article/details/51492105**](https://blog.csdn.net/eternity1118_/article/details/51492105)


