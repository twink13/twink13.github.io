---
published: true
subtitle: 如何脱离摄像机渲染物体
---
## 为什么不使用摄像机渲染物体
Camera.Render()接口被调用后,Unity帮助我们做了一系列操作,包括渲染目标的设置,Mesh级别可视区域剔除,摄像机的Layer可见性剔除,排序,设置MVP矩阵信息等等.
有些时候,我们希望渲染一些比较简单确定的内容,会觉得这个操作有些"重",因此需要有一种方法可以避免部分无关的计算.
利用CommandBuffer可以达到这个效果.

------
## 摄像机的渲染过程
1. 调用任意物体上的BeforeRender()函数
2. 调用Camera上的OnPreRender()函数
3. 计算摄像机的V矩阵和P矩阵,以及摄像机的世界空间位置
4. 设置渲染目标,如果在Camera里设置了Target那么就设置为这个RenderTexture,否则渲染到当前帧缓冲
