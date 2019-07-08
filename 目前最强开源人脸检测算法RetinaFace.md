## 目前最强开源人脸检测算法RetinaFace

原创： CV君 [我爱计算机视觉](javascript:void(0);) *昨天*

点击我爱计算机视觉标星，更快获取CVML新技术

------



人脸检测为目标检测的特例，是商业化最早的目标检测算法，也是目前几乎各大CV方向AI公司的必争之地。



WIDER FACE数据集是由香港中文大学发布的大型人脸数据集，含32,203幅图像和393,703个高精度人脸包围框，该库中人脸包含尺度、姿态、表情、遮挡和光照等变化。



![img](https://mmbiz.qpic.cn/mmbiz_png/BJbRvwibeSTvW5ibxEX4LV32nRp02urOEqS8af7FfXndZXnoLkH05EicS6QTe1uKdW7MrKjOn6R5jSKq5LKiaibTeJA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



WIDER FACE 几乎是目前评估人脸检测算法最权威的数据集。



RetinaFace 是今年5月份出现的人脸检测算法，当时取得了state-of-the-art，作者也开源了代码，过去了两个月，目前仅以极其微弱的精度差屈居第二名，但因为第一名的AInnoFace算法（来自北京创新奇智公司）没有开源，所以目前RetinaFace可称得上是目前最强的开源人脸检测算法。



![img](https://mmbiz.qpic.cn/mmbiz_png/BJbRvwibeSTvW5ibxEX4LV32nRp02urOEqWjiarbz6rCKibjqagLh2kHGh9RMn1JAneYLO0VftIiaGHHKh6ULbIosaw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



RetinaFace来自论文RetinaFace: Single-stage Dense Face Localisation in the Wild，作者来自帝国理工学院、InsightFace、Middlesex University London、FaceSoft。



![img](https://mmbiz.qpic.cn/mmbiz_png/BJbRvwibeSTvW5ibxEX4LV32nRp02urOEqMicVsWNQn6QKQOxgGTHwNFia2JUibZpzLPgT3VichHZ2J78vfovU4EIgibw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



相信很多朋友对InsightFace并不陌生，它是目前针对2D与3D人脸分析（含检测、识别、对齐、属性识别等）最知名和开发者最活跃的开源库。RetinaFace代码已经并入该库。



下图为在WIDER FACE 数据集上验证集三个子集的排名靠前的算法结果曲线和精度：



![img](https://mmbiz.qpic.cn/mmbiz_png/BJbRvwibeSTvW5ibxEX4LV32nRp02urOEqMxc4AEPF54Lf8ia6rTQBZGeo5WZiat7IiadB7LlUa9Wc1via3CBaRiaFSlw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



下图为在WIDER FACE 数据集上测试集三个子集的排名靠前的算法结果曲线和精度：

![img](https://mmbiz.qpic.cn/mmbiz_png/BJbRvwibeSTvW5ibxEX4LV32nRp02urOEqrvag9jiaSEFxK6J105I8d4PuiaZl2baO7y3UrVLibhTDJIl5M8GRicYa5g/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



在6个子集中，RetinaFace取得1个第一名，2个并列第1名，3个以极其微弱精度差屈居于第二名。



RetinaFace使用特征金字塔网络架构：



![img](https://mmbiz.qpic.cn/mmbiz_png/BJbRvwibeSTvW5ibxEX4LV32nRp02urOEqj8g2s23kKshbkmM3mTDQbC7Zo5ZGh4WNn6PiceAibEZuOxiar9xTtDHJg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



其主要创新点在损失函数的设计。



下图说明了RetinaFace的核心思想：



![img](https://mmbiz.qpic.cn/mmbiz_png/BJbRvwibeSTvW5ibxEX4LV32nRp02urOEq8ccoBvC9EyTNfKfLJRHSJGkbJWfmcBibpkZktn3qe7ODVBqQlgg5UsQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



在人脸检测多任务学习中，除了传统的人脸分类损失函数和包围框回归损失函数，作者额外标注了人脸 5 点信息，并以此引入人脸对齐的额外监督信息损失函数，还引入了self-supervised解码分支预测3D人脸信息分支。



集合了更多监督信息和自监督信息，是 RetinaFace 取得成功的关键。



很多时候，人脸检测是为了后续的识别，作者特意将检测结果送入人脸验证网络，在IJB-C test set上测试结果表明可以提高ArcFace的人脸验证精度(TAR=89.59% for FAR=1e-6)。



![img](https://mmbiz.qpic.cn/mmbiz_png/BJbRvwibeSTvW5ibxEX4LV32nRp02urOEqjuicRtnKVIb8dRdodBpd2L3xZb3R6F67rRGmCf36htPoj0bxzr7QyoQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



由上图可知，相对于MTCNN，在助力人脸验证上有一致性精度提高的表现。



更为难能可贵的是，使用轻量级骨干网络，RetinaFace算法在CPU上测试VGA图片可以达到实时。如下图：



![img](https://mmbiz.qpic.cn/mmbiz_png/BJbRvwibeSTvW5ibxEX4LV32nRp02urOEqcneXR6MpG2NBzGLjr5Eh4PZK2l7fe4hO3m5gxC9KmbLCDMCsU1NMbg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



感谢作者的开源，欢迎给大佬加星！



论文地址：

https://arxiv.org/pdf/1905.00641.pdf

代码地址：

https://github.com/deepinsight/insightface/tree/master/RetinaFace





------



**CV专业交流群**



52CV已经建立多个CV专业交流群，包括：目标检测、语义分割、姿态估计、人脸识别检测、医学影像处理、超分辨率、神经架构搜索、GAN、强化学习等，扫码添加CV君拉你入群，

**（请务必注明相关方向，比如：人脸检测）**

**![img](https://mmbiz.qpic.cn/mmbiz_jpg/BJbRvwibeSTv7ZnPMnOZ0WwM7DNjLlTdqfsdrzbObbTrIEnMDHLY6WBOHAJAJbozbEeLZLMicbicic7VQfP7IXQITw/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)**

喜欢在QQ交流的童鞋，可以加52CV官方**QQ群**：702781905。

（不会时时在线，如果没能及时通过验证还请见谅）

------



![img](https://mmbiz.qpic.cn/mmbiz_png/BJbRvwibeSTvVOnJBvePcP1qFUSWpyvrjpYAWNIZTZzUA7Zq4VPlReicJWcIeozxic5VhHlwNQNAFXmKQBtKf5xAQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

长按关注我爱计算机视觉

文章已于2019-07-08修改







![img](https://mp.weixin.qq.com/mp/qrcode?scene=10000004&size=102&__biz=MzIwMTE1NjQxMQ==&mid=2247487588&idx=1&sn=069dcd37a3182b039c7ff658e413fc40&send_time=)

微信扫一扫
关注该公众号