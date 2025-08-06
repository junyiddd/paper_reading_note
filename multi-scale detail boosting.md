【Sharpen】Dark image enhancement based on pairwise target contrast and multi-scale detail boosting

【论文链接】https://ieeexplore.ieee.org/document/7351031

【abstract】提出了1.全局enhance方法，2.全局enhance的基础上通过multiscale进行细节增强。(后者具体来讲主要是通过多尺度高斯差值金字塔（DoGs）实现局部细节增强)

methods

这里主要记录multiscale部分的技术细节，其他部分（全局增强）详见论文。

multi-scale detail boosting
<img width="571" height="553" alt="image" src="https://github.com/user-attachments/assets/478bb130-3162-4495-b687-343141c5e699" />

【key points】
- 首先使用不同大小的高斯核对全局增强后的影像I*进行模糊，得到三幅模糊后的影像
<img width="417" height="42" alt="image" src="https://github.com/user-attachments/assets/8acb4b06-fdbb-4a74-8c13-fde10b9739dd" />
<img width="571" height="48" alt="image" src="https://github.com/user-attachments/assets/aa406272-cb16-4131-bb51-9211734afe4d" />

- 然后，提取不同尺度的细节信息
<img width="466" height="36" alt="image" src="https://github.com/user-attachments/assets/88d336af-ac7a-4c02-a6e5-71ed28e9b3a8" />

- 加权融合不同层的细节，得到总的细节
<img width="506" height="52" alt="image" src="https://github.com/user-attachments/assets/7f185ff2-80dc-4e32-aaa9-c8baa186d07a" />

- 将D*加到I*上，实现细节增强

注意：
  1. 这里w1、w2、w3分别被设为0.5、0.5、0.25
  2. 当D*被加到I*时，D1上的细节扩充了影像中边缘附近的灰度差异，但可能会导致灰度过饱和
  3. 为了抑制饱和，对D1中的positive成分进行削弱，negative成分进行增强，但仍保持正负成分间的平均差异
