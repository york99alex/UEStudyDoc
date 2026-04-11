# 编辑器基础

## 界面

快捷菜单栏：选择、快速添加、蓝图、镜头、运行（Esc键退出运行）

总是推荐使用纯英文的编辑器
Edit编辑-Preferences编辑器偏好-搜索Language-Editor Language选择English

**世界场景设置**（World Settings）：

顶部菜单选择 窗口-世界场景设置，每个关卡都有独立的世界场景设置，将该面板添加到右侧可以进行关卡的各种设置，包括 游戏模式、调整关卡全局光照效果。
导入第三人称功能后，可以在此面板的 游戏模式-游戏模式重载中切换 BP_ThirdPersonGameMode

**Actor**：

所有可以放入关卡的对象都是 **Actor**，比如摄像机、静态网格体、玩家起始位置。Actor支持三维变换，例如平移、旋转和缩放。你可以通过游戏逻辑代码（C++或蓝图）创建（生成）或销毁Actor。

![image-20251107121957379](https://raw.githubusercontent.com/york99alex/Pic4york/main/fix-dir/2025/11/07/f4a464de78837eb4bec31b13e7a66f34-image-20251107121957379-fc61f0.png)



**Component**

组件，在某种意义上，**Actor** 可被视为包含特殊类型 **对象**（称作[组件](https://dev.epicgames.com/documentation/zh-cn/unreal-engine/components-in-unreal-engine)）的容器。 不同类型的组件可用于控制Actor移动的方式及其被渲染的方式，等等。Actor的其他主要功能是在游戏进程中在网络上进行属性[复制](https://dev.epicgames.com/documentation/zh-cn/unreal-engine/actors-in-unreal-engine#replication) 和函数调用。

![image-20251107143617459](https://raw.githubusercontent.com/york99alex/Pic4york/main/fix-dir/2025/11/07/8f6194390d522a95dc1452916925d640-image-20251107143617459-1a4add.png)

> 虚幻就是一个舞台，Actor就是台前幕后的"演员"，Component组件就是演员的各种能力，有基础的也有各自独特的



**内容侧滑菜单**

又叫库、资产库、内容浏览器，ctrl+space 打开。
在关卡中ctrl+s只是保存关卡，内容浏览器里的==保存所有(ctrl+shift+s)==更重要

在**内容**中可以添加各种资产，比如功能或内容包

在进行导入资产时，相应文件会被导入到临时文件空间中，对应的文件预览图会有一个星号*，此时记得点击保存所有，完后才是真正导入到了项目空间中（转换为.uasset文件等）



## 模型操作

从内容浏览器通过滤静态网格体或者快捷菜单栏的 添加-形状-球体，拖拽到场景

**变化**快捷键：

选中物体后，w开启移动，e开启旋转，r开启缩放，按空格循环切换。end键会让物体落到平面上
在==移动时按住shift==，可以保持物体在水平/垂直方向移动，并且保持视角跟随于物体，可以更高效的进行移动拖拉

F键，focus，聚焦到Actor
复制：alt+移动拖拉，或者ctrl+d
多选：ctrl加选中，可加可减
临时移动原点：鼠标中键拖拽物体坐标轴可以临时移动其原点，可配合多选更快捷地调整
角点吸附：按住v键移动，适用于整数倍方块几何的移动，比如墙面等

**原点**，又叫轴心，一个基本模型的中心点，同样的球体资产，有的球体原点在中心，有的在表面，而在表面的可能更容易进行一些对其表面的移动操作。通过双击对应资产，打开静态网格体编辑器预览，在视口预览选项中勾选 显示枢轴，则可看到基于原点的坐标轴（快捷键 alt+p）
![image-20251107154001855](https://raw.githubusercontent.com/york99alex/Pic4york/main/fix-dir/2025/11/07/9e96ea4ce4a95c9dce3b633f3b022553-image-20251107154001855-e1e94b.png)

(在外部模型导入时, 也需要注意原本模型的单位轴和世界中标等重合)



## 资产

导入和迁移资产，都需要注意根路径的问题，以Content为准。

从其他项目迁移资产到自己的项目：

1. 先在其他项目中找到对应的模型/贴图等，选中在其细节里“浏览到内容浏览器”
2. 右键资产，资源操作-迁移，默认确定（也可直接迁移文件夹）
3. 选择路径时，直接选择到需要迁移进的项目的Content目录
4. 有问题或不放心，可以在迁移后的文件夹右键-**修复重定向器**



### Bridge

Quixel Bridge，快速添加到项目。是虚幻官方的提供高质量的3D扫描资产、纹理和材质的平台。

202501，Bridge需要收费证书，直接使用Fab。

- **3D Assets**：3D模型资产，自然、建筑、道具、工业等。
  - 资产的详细页面描述：
    - Size：模型相对人的大小和尺寸。
    - Open/Closed：模型是否完全封闭或者有开口。完全的Closed的圆就表示模型的表面是“无缝”、无开口的。
    - Quaility：Low、Medium、High，部分模型有最高的Nanite纳米级，Nanite可配合引擎到达最极致的效果。
- **3D Plants**：3D 植被。特点，响应引擎的风力系统。
- **Surfaces**：表面/材质，比如路面、石板、草地等，有无缝衔接的特性。
- **Decals**：贴花，增加细节，打破模型、材质的重复感，用于覆盖在模型表面制造真实和氛围感。
- **Imperfections**：纹理，指纹、划痕、灰尘层、抹痕、油渍等黑白纹理。连接到材质节点的 Roughness（粗糙度） 或 Metallic（金属感） 通道，提供更高级的视觉质感。



## 材质



### 材质球 Materials

材质球是贴图和模型之间的媒介，贴图需要通过着色器中原有的光照算法，将贴图中的数字信息和颜色信息转化为视觉效果并进行渲染。

在初学者关卡 ==StarterContent/Map/StarterMap== 里有各种静态和动态的材质演示。

**贴图** ==> **材质球** ==> 应用到**模型**表面进行渲染



### 材质编辑器

默认的**材质结果节点**，以**PBR** (Physically-Based Rendering) 基于物理属性的引擎渲染，通过特殊的光照算法，模拟光线射到物体表面时所展示出的类似真实世界的金属度、粗糙度等物理属性的引擎渲染方法。

- 金属感：
- 粗糙度：粗糙度为0是光滑的镜面反射，为1则是完全粗糙的漫反射。

#### 节点操作

- 创建常量 Constant：
  - 按住1鼠标左键，1维常量
  - 按住2鼠标左键，2维向量
  - 按住3鼠标左键，3维向量，可连接到基础颜色，调节颜色。
- 常量转为参数，对外部暴露：右键常量节点，转换为参数，命名
- ==UV节点==：UV 是一套将 2D 坐标映射到 3D 表面上的“地址索引系统”，在引擎底层，UV 实际上是存储在 **顶点（Vertex）** 上的属性数据。而UV 空间就是一个标准的二维笛卡尔坐标系，具有重复、截断、镜像的特点。
  1. Tiling (平铺/缩放)数学操作： UV * 2
     结果： 贴图在模型上变小了，重复了 2 次。因为原本 [0, 1] 的范围现在变成了 [0, 2]。
  2. Offset (偏移/位移)数学操作： UV + 0.5
     结果： 贴图位置发生了移动。
  3. Panner (平移旋转)数学操作： UV + (Time * Speed)
     结果： 贴图在表面滚动起来了，比如动态水体或传送带的核心逻辑。

- [**黄金树效果实战**](https://www.bilibili.com/video/BV1nA4y1f7eh?t=586.5)，包括自发光材质、菲涅耳表达式、遮罩、蒙版、树叶抖动。

### 纹理/贴图 Texture

纹理也分多种作用类型，一般与其命名的后缀有联系。

- 底色：Diffuse, BaseColor, Albedo, D, BC
- 凹凸：disp。多用于不平整的表面增加
- 粗造度：rough，灰度贴图（仅黑白），原理是为每个纹理像素指定其粗糙度。
- 法线：nor（Normal），原理是在凹凸表面的每个点上均作发现，通过RGB颜色通道来标记发现的方向，用低廉的计算成本，让平整的模型表面看起来具有复杂的凹凸细节。看起来通常是紫蓝色的。

### UV贴图空间

纹理贴图空间的简称，可以理解为贴图空间的大小，UV值越大，贴图密度越高。
快捷键u创建uv数值节点



## 光照

影响范围较小，相对可控：

- 点光源：球形的光源，理解为恒星太阳。
- 聚光源：俗名射灯，有一个固定朝向的光源
- 矩形光源：结合上面两点，可控制朝向和范围，效果又更像点光源，理解为摄影镁光灯/补光灯

影响范围较大：

- 定向光源
- 天空光照



### 基本概念（区域光照）

- 强度：光线的明亮度
- 光源颜色
- 衰减半径：影响范围
- 源半径：光源本身的半径，影响其照射物体的影子的虚实
  - 源半径为0：<img src="https://raw.githubusercontent.com/york99alex/Pic4york/main/fix-dir/2026/01/12/1e8e0b3097acefec14ce14275d776f1f-image-20260112102911096-fc277e.png" alt="image-20260112102911096" style="zoom:50%;" />
  - 源半径为50：<img src="https://raw.githubusercontent.com/york99alex/Pic4york/main/fix-dir/2026/01/12/977f373b036661d1aed6ae22773bce0a-image-20260112103146670-66e815.png" alt="image-20260112103146670" style="zoom:50%;" />

特有的：

- 聚光源
  - 锥体外部角度：照射区域的大小，聚光的范围
  - 光源描述文件：可以使用自带提供的几个IES纹理描述来达到更丰富的光线效果
- 矩形光源
  - 挡光板角度：在照射范围边缘有一些模糊的虚影，范围由该参数控制



### 环境光照

菜单栏-窗口-**环境光混合器**：在这个编辑器窗口中可以创建和编辑关卡的天空、云、大气光源和天空光照。

注：所有环境光照的操作都会实时地影响整个关卡的效果，也即动态实时的天气系统

- 定向光源：又名大气光源、太阳光、平行光。（空场景确保==优先创建此项==）
  - 参数-源角度：控制太阳的大小，影响影子模糊。
  - 操作-调整太阳光角度：两种
    - 第一种：选中 DirectionalLight，按e键进行旋转操作，三个周都可以
    - 第二种：选中，按住Ctrl + L呼出罗盘指针的同时移动鼠标，更自由也更灵敏的控制
- 天空大气：天空的背景
- 体积云：云朵，让天空更加丰富
- 天空光照：可以将天光的一些信息重新映射回场景（空气散射），提供更自然的光照，包括大气层散发的蓝色微光以及整个环境的反射光。



### HDRI背景

封装好的环境插件：菜单栏-窗口-插件-搜索 HDRIBackdrop，重启虚幻5后，在快速添加-光源-HDRI背景

将高动态范围（HDR）图像用作背景，通常用作展示模型

- Intensity：光照强度
- Size：背景大小
- 高级-Use Camera Projection：使用摄像头估算，背景变得自然减少拉伸
- 背景图也可以在 [HDRI • Poly Haven](https://polyhaven.com/zh/hdris) 寻找HDRI



### 后期盒

快速添加-视觉效果-**后期体积处**/PostProcessVolume，俗称后期盒

- 作用范围，其Box大小就是作用范围
  - 可以通过缩放调整大小，被包裹起来的范围就会受到后期盒配置属性的影响
  - 也可以在细节中搜索Bound，勾选启用无限范围
- **眼部自适应**：人眼在亮暗差异较大的情况下过度时，会自动调整眼球细胞对光线的敏感度，从而更好的观察和适应环境，在虚幻引擎中，为了实现这一效果，设计出了**自动曝光**这一功能，但对于一些本身明暗变化较小的单一环境，可能会引起对于场景中光照强度的误判，可能需要调整或关闭这一功能
  - 通过后期盒，Exposure - Max/Min EV100，都设置为0则关闭自动曝光
- 后期处理材质：设置与后期处理一起使用的材质，以创建破坏的视觉屏幕效果、区域类型效果，也可以实现游戏的整体外观风格（比如：无主之地的美漫风）
- 色差强度 Chromatic Aberration：模拟镜头、色散的效果
- Image Effects：类似于暗角
- 色温 Temperature：冷暖色调

#### 后期调节

颜色基础认知：

- 色彩心理
- 冷暖变化
- 色彩属性

色彩工具网站：http://bj.91join.com/color.html

颜色调节思路：

- 统一整体颜色表现，把控画面情绪氛围
- 协调冷暖对比，适当增强明暗关系中的冷暖关系

调节流程及常用参数

- 颜色分级表现
  - 色温/白平衡
  - 全局Global，中间调，阴影，高光
- 镜头辅助效果
  - 辉光/光溢出
  - 曝光
  - 光斑
  - 暗角
  - 镜头脏迹
  - 色调分离
  - 镜头景深
    - 光圈
    - 焦距
- 一键调节，可理解为滤镜，Misc - 颜色分级LUT，需要导入LUT资产



### ==Lumen==

全动态全局光照和反射系统，高质量的解决了全局动态光中的问题，包括了全动态的色彩溢出、间接照明、间接阴影等，并且支持无限的漫反射。（UE5的门面技术）

开发者和玩家(游玩中)可以实时照亮或变暗场景中的区域，减少光照层面上的美术表现得难度，或者进行与场景更真实的交互。

UE4效果：只有直接光照（UE4可以通过静态烘焙达到类似UE5的效果，额外成本）
<img src="https://raw.githubusercontent.com/york99alex/Pic4york/main/fix-dir/2026/01/12/9a99e14f7015e1538058d45be9e3e6a7-image-20260112121550682-0a6545.png" alt="image-20260112121550682" style="zoom:50%;" />

UE5效果：
<img src="https://raw.githubusercontent.com/york99alex/Pic4york/main/fix-dir/2026/01/12/441af2820131659af07760a032e9b116-image-20260112121706542-9b45b3.png" alt="image-20260112121706542" style="zoom: 50%;" />



### 体积光

如何要应用射灯、光照等的**体积散射强度**，达到雾气散射的效果（丁达尔效应）

- 后期盒中勾选启用**体积雾**
- 射灯里勾选启用**投射体积阴影**，可以将照射的光照受到物体遮挡的影响

**技巧**：

如何让一个光源打出多个光束，在光源前放置一个立方体，完全遮挡住以后，把某个树叶材质应用到立方体上，立方体就会变成很多树叶，从而透出多个自然的光



### 光照通道

Lighting Channel，每个光源和每个网格体都有三个通道开关0、1、2，默认都处在通道0。
**规则**：只有当光源和物体的通道“对上”时，该光源才会对该物体产生影响。

应用场景：一些不太符合物理规律但是又能有更好更适合的美术表现，让光源只对特定物体生效，比如提亮主角、眼睛、主要物品等。

需要注意，通道是否匹配并不影响阴影投射，如果你关闭了一个物体对某个光源的通道，该物体确实不会被照亮，但它**依然可能投射阴影**（如果光源开启了阴影投射，也可以手动关闭）



### 视图-光照

在视图右侧的光照选项中，可以切换当前视图的光照模式：![image-20260127142119344](https://raw.githubusercontent.com/york99alex/Pic4york/main/fix-dir/2026/01/27/03b8ed016862d08295d609b62e17c119-image-20260127142119344-200de0.png)

- 光照：正常的环境效果
- 无光照：剔除掉所有光照，仅保留材质本身的底色影响
- 仅光照：只有灯光光照的表现，不会包含模型自身的纹理信息所影响的环境效果
- 细节光照：区别于全光照，细节光照下所有的模型都是白模，剔除模型的底色，可以看到模型的粗糙、金属、反射等



## 地形

在关卡下方的菜单栏-选择模式中，选择地形模式，进入地形编辑

左侧，创建一个默认配置的地形（该地形模块，本质也是一个特殊的模型 landscape，或者说网格体）

除了通过该方式进行手刷操作、还可以通过外部软件制作地形地貌：Worldcreator、Worldmachine、houdini、Gaea，将以高度图的方式贴附到当前关卡的地形模块上去生成

### 雕刻

也即手刷，雕刻有多种工具和多种笔刷

- 雕刻，笔刷，其中第二种Alpha笔刷比较适合山脉地形的生成
- 抹除、平滑
- 平整：长按拖动，以开始时的高度为目标进行平整，也有选项-高平目标，可指定平整高度
- 侵蚀：弱化平滑
- 水刀：适合边缘、有落差的地形塑造
- 噪点：随机调整

快捷键 `[` 和 `]` 可调整笔刷大小



### 地形材质

1. 先创建材质
2. 节点MakeMateriaAttributes：将多组纹理应用到多个材质球上
3. 节点LandscapeLayerBlend：将多个纹理或材质网络混合在一起作为地形图层
4. 选择材质球终节点，勾选 细节-使用材质属性，将第2步的输出连到终节点的**材质属性**上
5. 应用，先选中地形，将材质创建的材质实例拖动到地形上（如无效确认是否选中，或者在细节中找到地形材质，进行应用）
6. 再回到地形模式-绘制，目标层（如果没有刚才节点创建的对应层，在层的操作一栏点击-**创建所有材质层**
7. 此时选中指定层进行绘制

也可以下载网上的地形材质资源



## 植被系统

同地形编辑，进入植被模式，添加植被资产（也是一种特殊的静态网格体），此外地形系统和植被系统统称为景观系统。

对齐法线：是否需要垂直于其所在的地形平面需要根据不同植被来选择，灌木可能可以垂直，树木则不需要

LOD：Layer Of Detail，多细节层次，该技术会根据模型节点在显示中的位置和重要度决定渲染资源的分配。比如离远了看的就不那么清晰就可以使用减面更多的模型。



## ==Nanite==技术

如上面所说，在传统的开发中，每个模型都需要制作多层LOD，伴随着LOD层数增加其模型的面数也要减少，从而达到优化渲染时间的效果，但随着性能提升和对美术效果需求的提升，LOD在过度时明显的变化及LOD提高导致表现得大量缺失也是一个问题。

虚拟化几何体技术，Nanite 会将模型拆分成每个通常包含约 **128 个三角形** 的“集群”，通过实时分析屏幕只渲染在屏幕像素尺度上可见的细节，让场景可以直接使用数以亿计的多边形（如高模、电影级影视资源），而不需要担心传统引擎中的性能瓶颈。

### 优缺点

优点显而易见，极致的视觉体验，但并非完全没有缺点：

- **硬盘空间**：虽然 Nanite 压缩率很高，但 100 万面的模型肯定比 1 万面的大。如果全线使用高模，你的项目包体（Packed Build）会迅速膨胀。
- **内存压力**：Nanite采用流式传输，高模数据在运行时需要从硬盘流送到内存，如果硬盘性能不足，在大场景快速移动时可能会看到模型“模糊”或加载延迟。



**建模软件** DCC (Digital Content Creation) ：Auto desk里的MAYA、Max，Zbrush



### 导入Nanite模型

NM前缀，导入高面数时建议转为Nanite，通常建议将面数大于 **2000** 的物体都转为 Nanite。虚幻也有内置的Nanite分析工具、审计工具分析模型是否适合开Nanite。

导入成功后，右键模型资产，可以检查是否使用Nanite



## 虚拟阴影贴图

VSM，可以提供稳定的高分辨率阴影，通常与Nanite、Lumen以及世界分区功能结合使用，为大型开放场景提供光照。



# 地编教程



## 参考图与资源

有目标有需求才有具体的地编落地实现，美术、CG网站，见[参考链接](#链接)



## 天空大气

可以通过手动创建天空球使用对应材质（调整氛围颜色）、编辑[环境光照](#环境光照)、使用[后期盒](#后期盒)处理等来综合调整。

天空球的制作：https://www.bilibili.com/video/BV1wU4y1U7Sc?t=457.4 （法线向内的球体）



## 开放世界地形



### 高度图

可通过 WorldCreator、WorldMachine、Gaea、Houdini 制作（上手难度递增）

在地形模式，左侧 从文件导入
高度图是灰度贴图，仅有黑白色调，颜色越白表示高度越高，越黑则表示越低。



## 雾效

大气雾是整个环境的雾气底色，而==片雾==则是有点睛去表达体积感和景深的作用。

片雾：本质上是一个带有透明材质的平面（Static Mesh Plane）或粒子（Particle），通过一张带有噪声（Noise）的贴图和透明度算法来“伪装”成雾气。



# 摄像机

通过快速创建-过场动画-电影摄像机Actor，来创建摄像机。

对于16：9的画面，适应人眼的焦距是在12~15左右

操作: 选中摄像机，右键 控制Camera，可以固定以摄像机视角的窗口，配合多窗口视图（主菜单栏-窗口-视图）有助于摆放等地编工作



# 镜头

镜头其实也是一种表达方式，一种叙述语言，与电影中的镜头同理

- 取景：远景、全景、中景、近景、特写
- 镜头运动方式：固定镜头和运动镜头（推、拉、摇、移、跟、升、降等，以及变焦聚镜头（希区柯克式变焦）等）
- 镜头时长：短镜头、长镜头

## Sequence定序器

关卡菜单栏中 - 添加关卡序列
![image-20260127160247174](https://raw.githubusercontent.com/york99alex/Pic4york/main/fix-dir/2026/01/27/5728e9671d126e0919d2b6df1b823e29-image-20260127160247174-de95f2.png)

添加关卡序列以后会自动打开Sequence视图，新建摄像机，根据当前画幅调整焦距，16：9的画面适合12~15的焦距

![image-20260127160503571](https://raw.githubusercontent.com/york99alex/Pic4york/main/fix-dir/2026/01/27/0ed2f553ee3c5c4900e05d6f11d26bb6-image-20260127160503571-e0fa67.png)

尝试做一个节奏偏缓的10秒的推的、长镜头

1. 选择变换Transform，在当前帧/初始帧创建关键帧（俗称K一帧）
   ![image-20260127160949668](https://raw.githubusercontent.com/york99alex/Pic4york/main/fix-dir/2026/01/27/cb3212d3df64e82f8226b4412422a2f8-image-20260127160949668-f08282.png)
2. 时间轴的单位为帧，一秒30帧，默认150帧，调整总时长。
   点击CineCameraActor右侧的镜头按钮，切换到该镜头控制视图
   <img src="https://raw.githubusercontent.com/york99alex/Pic4york/main/fix-dir/2026/01/27/5447796baa48ec3ea95a547010cb16c2-image-20260127162346307-41e1d5.png" alt="image-20260127162346307" style="zoom:67%;" />
3. 上方视图为摄像头控制视图时，我们在变换轨道上的第0帧k一帧，然后移动当前时间轴至最后，在上方控制视图中移动镜头位置至目标点（比如向前移动），然后在最后一帧k一帧，此时两个关键帧相连，点击上方摄像头镜头视图中的播放按钮，画面就开始移动了。
4. 可选：影片场景捕获，将所得到的镜头画面导出为视频
   ![image-20260127162736478](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20260127162736478.png)
   添加Movie Render Queue插件可以将影片打板为图片序列，并且在输出时提供更多选项达到高精度等效果



# 蓝图BluePrint

## 蓝图类BluePrint Class

- **Actor**：一个可被放置和生成在场景中的物体，包括但不限于箱子、房屋、载具、摆件等。
- **Pawn**：继承自Actor，可被玩家或AI附身/控制（Possess），并不一定是生物，比如载具或AI单位等
- **Character**：继承自Pawn，转为双足人形生物设计的，自带以下三个核心组件：
  - CharacterMovementComponent (移动组件)：内置了极其复杂的行走、跳跃、下落、游泳和飞行逻辑，且支持完美的网络预测同步
  - Capsule Component (胶囊体)： 预设好的物理碰撞形状
  - Skeletal Mesh (骨骼网格体)： 预设好的渲染层级
- **Player Controller**：控制器，通常为玩家或者AI，Controller是灵魂，Character是肉体，通过附身Possess进行连接。



## 蓝图概念

- **Variables变量**，注意新建变量以后需要编译才可以进行进一步设置
  - 变量类型
    - 基础逻辑与数值：
      - Boolean布尔
      - Integer整数
      - Float浮点数
    - 字符文本：
      - Name名称：被内部索引化的字符，比较Name远快于比较String
      - String字符串：调试文本或拼接、替换、切割，灵活但开销大
      - Text文本：UI专用，==唯一支持多语言本地化==
    - 空间变化
      - Vector向量：x, y, z
      - Rotator旋转量：Roll翻滚角, Pitch俯仰角, Yaw偏航角
        <img src="https://raw.githubusercontent.com/york99alex/Pic4york/main/fix-dir/2026/01/29/ed62567826f956c471912353853be451-9080a58875e091bda30c3fdac4ec66d7-356ab5.png" alt="img" style="zoom: 80%;" />
      - Transform变换：用于Spawn Actor，包含完整的位置Location、旋转Rotation、缩放Scale
  - 对象类型 Object Types，其引用类型
    - Object Reference 对象引用，实例指针，比如存储玩家或场景中具体存在的实例
    - Class Reference 类引用，蓝图、C++类的指针，比如告诉引擎我需要生成哪种物体
    - Soft Object Reference、Soft Class Reference：软引用，区别于上面两个强绑定，比如A蓝图引用了B资产，那么只要A载入内存，B也要跟着载入；而软引用，则是存储资产的路径，不会自动加载，需要手动调用 Async Load Asset（异步加载），等加载完毕以后才能转为直接引用/硬引用来使用。
      - 如果你确定这个东西“必须一直存在且响应极快”，用 **Hard**。
        如果你不确定这个东西什么时候会出现，或者它很大，用 **Soft**。
  - 变量的容器类型 Container
    ![image-20260129115001539](https://raw.githubusercontent.com/york99alex/Pic4york/main/fix-dir/2026/01/29/83c30c700d09ec5bb36f3bfc4661d4b2-image-20260129115001539-fcce3e.png)
- **Function函数**，可选的输入或输出，封装一系列的操作与命令
- 父类子类，继承与重写，私有公有访问域等略

### 事件图EventGraph

默认的几个事件：

- Event BeginPlay 当蓝图创建时的事件
- Event Tick 每一帧都会调用的事件

### 节点

常用节点，通过引脚和入角拉线

- Sequence 通过添加pin脚，按顺序执行一系列的操作
- 循环
  - For Each Loop 
  - For Loop
  - While Loop
- Branch 条件语句，相当于If
- IsValid 合法值判断

**==快捷键==**

- 注释：习惯为蓝图进行区域整理与注释，框选后快捷键C
- 整理：多选，快捷键Q进行齐平整理
- 连线节点：双击连线可以在连线中创建一个节点，用于整理连线，该节点可拖动

### 自定义事件

Add Custom Event，命名后可跨蓝图在另一个事件图中搜索事件名进行订阅



### 蓝图调试

1. Print 打印
2. BreakPoint 断点调试，右键需要断点的节点，Add BreakPoint，蓝图运行时如果达到该断点则会停住，快捷键F9
3. Watch Values，在蓝图节点间或变量引脚右键，选择Watch this value监视此致，静态观察，不需要中断游戏

## 增强输入

[虚幻引擎中的增强输入 | 虚幻引擎 5.7 文档 | Epic Developer Community](https://dev.epicgames.com/documentation/zh-cn/unreal-engine/enhanced-input-in-unreal-engine)

增强输入系统主要有四个概念：

-  **输入动作（Input Actions）** 表示可以执行的某个操作的意图，通过定义不同类型来确定行为，
  - ValueType：比如移动是2维Axis2D，跳跃是布尔动作Digital(bool)
-  **输入映射上下文（Input Mapping Contexts）** 输入动作的集合，将动作意图与按键关联起来，描述了给定输入动作的触发规则。映射上下文可以动态地为每个用户添加、移除或安排优先次序。
  - 层级结构，上层为输入动作，动作层下面是用户的输入，比如按键、按钮等
-  **输入修饰器（Input Modifiers）** 
-  **输入触发器（Input Triggers）** 

## 第三人称移动实战

参考视频：[添加与配置增强输入系统](https://www.bilibili.com/video/BV1Fy411v7gm?p=3)

1. 定义意图，创建 Input Action 资产

   - `IA_Move` 移动，将 Value Type 设置为 Axis2D
   - `IA_Look` 转动视角。Value Type 同样为 Axis2D
   - `IA_Jump` 跳跃。保持默认的 Digital (Bool) 即可

2. 绑定按键，连接意图与键盘输入，创建 Input Mapping Context 资产 IMC

   - 默认Default Key Mappings 中添加映射：
     - 选择 `IA_Move`：绑定 **W** ，Modifiers添加元素，即对输入的修改，默认X轴正，所以 w 无需操作， **S** (Negate负值), **A** (Negate + Swizzle Input Axis Values 交换xy轴输入，选择YXZ，将x轴的输入修改为-y轴), **D** (Swizzle Input Axis Values默认YXZ)。
     - 选择 `IA_Look`：绑定 **Mouse XY 2D-Axis**。
     - 选择 `IA_Jump`：绑定 **Space Bar**。

3. 添加眼睛，第三人称视角镜头

   1. 添加组件： 点击左上角 +Add，搜索并添加 Spring Arm (弹簧臂)。

   2. 添加相机： 选中 Spring Arm，再点击 +Add 添加 Camera。这样相机就会乖乖跟着弹簧臂走，不会穿模。

   3. 配置旋转：

      - 选中 BP_MyCharacter (Self)，在细节面板取消勾选 Use Controller Rotation Yaw（否则转视角时角色也跟着转）
      - 选中 Character Movement 组件，勾选 Orient Rotation to Movement（这样角色转身时，身体会朝向移动方向）
      - 选中 Spring Arm，勾选 Use Pawn Control Rotation（这样鼠标动，相机才动）

      *结构*：![image-20260129173309961](https://raw.githubusercontent.com/york99alex/Pic4york/main/fix-dir/2026/01/29/05bf05f949a362f2a77486778ee18cca-image-20260129173309961-0fadc7.png)

      

   4. 编写神经，让动作输入事件产生实际的效果

      1. 在World Settings中，将GameMode Override更改为自己创建的蓝图游戏模式GameMode类，将默认控制者Defauilt Pawn Class选择为之前创建的蓝图Character类（与在蓝图GameMode类中修改一样）
      2. 在BP_MyCharacter事件图中，为玩家控制器注册IMC上下文
         ![image-20260129173727119](https://raw.githubusercontent.com/york99alex/Pic4york/main/fix-dir/2026/01/29/5acb7e46f4f14b619060ab5cee590f6b-image-20260129173727119-a4ce5d.png)
      3. 处理移动，在BP_MyCharacter事件图中，右键搜索节点 IA_Move ，选择 Input - Enhanced Action Event 下的 IA_Move，下图中 Action Event的出脚Action Value右键 Split Struct pin直接转为了x、y参数，x轴前后的移动，y轴对应左右，右手方向为y轴正轴
         ![image-20260129174541069](https://raw.githubusercontent.com/york99alex/Pic4york/main/fix-dir/2026/01/29/172697e06a2f09d126db07072e0056c8-image-20260129174541069-01bc72.png)
      4. 这一步点击保存与编译再Play就可以实现wasd的运动了
      5. 右键搜索 IA_Look 事件
         直接连接到 Add Controller Yaw Input (对应 Action Value X) 和 Add Controller Pitch Input (对应 Action Value Y)
      6. 补充：
         1. 如果添加俯视等仰角变化时，以俯视注视角色同时移动时发现角色移动不动，是因为 Add Movement Input 的 World Direction获取时传入了额外维度的数据，其实只需要z轴，拆分一下引脚输出和输入即可修复。
         2. 一些意外的物理碰撞、受力或动画偏移可能导致即使输入只在一个轴上玩家角色的实际移动可能还是会出轴/出轨，可以在 BP_MyCharacter 自定义的角色类的 Components - CharacterMovement Component 的  Details（细节） 面板中搜索 "Planar"，勾选 Constrain to Plane (约束至平面)。将 Plane Constraint Normal 设置为：(0, 1, 0) 锁定平面指向的法线向量（x, z为0）。将 Set Plane Constraint Origin 保持在 Y=0。



## 协作: 版本控制

Revision Control

协作时先配置Git, 蓝图编辑窗口右下角 Revision Control - Change Revision Control Settings 配置git路径 (cmd 执行 where git 输出路径)

版本控制信号: 

- 绿色对勾, 表示文件最新
- 红色问号, 新建资产, 还没有被 Git 追踪
- 蓝色加号, 资产已添加, 但还未第一次提交
- 感叹号或者勾选符号, 资产已被签出(Checked Out), 本地可写, 等待修改提交

当修改蓝图并尝试保存时，弹出 **Check out assets** 窗口，这是虚幻引擎保护资产的一种机制。
在此之前, 本地资产都还只是只读, Check Out 以后会被服务器(或LFS)记录下占用。
当你尝试修改一个别人已经 Check out 的资产，虚幻会弹出警告，提示“该资产已被 [用户名] 锁定”。

**最佳实践**

1. 开始修改前，先编辑资产，保存触发 Check out，确认 Make writeable
2. 修改中，及时频繁地编译 Compile (蓝图)
3. 修改结束，Save资产，在内容浏览器中右键 Revision Control - Check In 或者蓝图编辑器右下角 Revision Control - Check In



# C++

## 语法清单

C++作为一门提供”绝对控制权“的工业级编程语言，其入门上手并不容易，虽然虚幻引擎中的C++是高度封装定制、自动化后的，但也建议在虚幻里进行C++从零开始的开发前，先系统性完整性地单独学习原生C++语言，至少学习掌握以下语法：

1. **内存管理**：
   - 指针、引用
   - 堆、栈
   - 空指针
2. **类与面向对象**：
   - 构造函数、析构函数
   - 继承与多态
   - 虚函数、重写
   - 访问控制
3. **预处理器与宏**：
   - 基本宏定义
   - ==**反射**==
4. **现代 C++ 特性**：
   - `auto` 关键字
   - 常量正确性 (`const`)
   - 枚举类 (`enum class`)：强类型枚举
   - 基础容器：熟悉 `std::vector` 和 `std::map`， 对应到UE里的 `TArray` 和 `TMap` 等
5. **编译原理基础**：
   - 头文件与源文件



## 常用方法

- format C++20格式化方法

  ```C++
  // 自动推导：
  std::format("玩家：{}，等级：{}，胜率：{}%", "云天明", 99, 98.5);
  // 对齐填充
  std::cout << std::format("|{:_<10}|", "左对齐") << "\n"; // |左对齐_______|
  std::cout << std::format("|{:*>10}|", "右对齐") << "\n"; // |_______右对齐|
  std::cout << std::format("|{: ^10}|", "居中") << "\n";   // |    居中    |
  // 控制精度与符号：
  std::format("PI is {:+.2f}", pi); // PI is +3.14
  ```

- 



## 反射

**学习建议清单**

| **优先级** | **内容**                               | **学习目标**                            |
| ---------- | -------------------------------------- | --------------------------------------- |
| **P0**     | **工厂模式与字符串映射**               | 实现 `CreateObject("MyClass")`。        |
| **P1**     | **C++20 Concepts / type_traits**       | 掌握编译期类型检查，这是反射的基石。    |
| **P2**     | **虚幻 `FindField` 与 `ProcessEvent`** | 在运行时通过反射修改属性或调用函数。    |
| **P3**     | **三方库研究 (RTTR 或 PFR)**           | 看看纯 C++ 社区是如何不靠宏实现反射的。 |



## Rider笔记

### 快捷键

可从vscode或者idea等习惯迁移

- 全局搜索 双击shift
- 全文搜索/文件中搜索 ctrl + shift + f   替换 ctrl + shift + h
- 打开最近的文件 ctrl + e
- 定位当前打开的文件所在的文件位置 alt + f1 选择资源管理器



## Specifier & meta

**Specifier** 标识符 

- BlueprintCallable 暴露到蓝图中可被调用
- BlueprintNativeEvent 原生蓝图事件，可进行覆盖调用

**meta** 元数据说明符 

- 函数默认参数值
  - 仅在蓝图节点中设定默认值  CPP_Default_ParamName
  - 用法：UFUNCTION(BlueprintCallable, meta = (Location ="4,5,6")) 可以指定蓝图中该方法的Location的默认参数，避免在C++尾部默认参数的语法
- EditCondition表达式 用表达式计算来控制是否可被编辑
- TitleProperty 结构数组元素标题，自定义结构美化直观
  - meta = (TitleProperty = "{MyString}[{MyInt}]") 
- CommutativeAssociativeBinaryOperator 二元运算符，Add pin来实现嵌套
- Variadic 可动态的多输入多输入



## 示例

- UE_LOG 打印日志

  ```c++
  UE_LOG(LogLyra, Warning, TEXT("ClassName: %s"), *GetName());
  // 频道或者说分类，级别，格式文本，格式参数
  ```

- 屏幕调试日志

  ```C++
  GEngine->AddOnScreenDebugMessage(-1, 5.f, FColor::White, TEXT("This is an Example on-screen debug message."));
  // 消息id防止重复，显示时间，颜色，格式文本，格式参数
  ```

- 每Tick进行旋转和上下移动
  ![image-20260409142754151](https://raw.githubusercontent.com/york99alex/Pic4york/main/fix-dir/2026/04/09/b51c4aad69a41fac1765958652b9ad02-image-20260409142754151-0b8715.png)

- [使用定时器](https://dev.epicgames.com/documentation/unreal-engine/using-timers-in-unreal-engine?application_version=5.5)

- [断言](https://dev.epicgames.com/documentation/unreal-engine/asserts-in-unreal-engine?application_version=5.6) 

  - check()、checkf() ，开发中会运行检测并触发崩溃，在发布中会自动移除

  - verify 开发版本中类似于 check，但在发布中也会运行，只是不会进行崩溃处理

  - ensure 用于处理非致命错误，所有版本都会运行但也都不会进行崩溃处理，但是会联系崩溃报告器，可获取触发信息


  










# 控制台命令

- 属性细节面板查看效果
  - 测试某个类 testprops class=xxx
  - 测试某个结构 testprops struct=xxx
  - 总的测试用例 testprops generator



# ==命名规范==

对于所有资产，统一采用 [类型首字母大写缩写]_[帕斯卡命名]
对于所有变量、函数等基本采用[帕斯卡命名](https://baike.baidu.com/item/%E5%B8%95%E6%96%AF%E5%8D%A1%E5%91%BD%E5%90%8D%E6%B3%95/9464494)

## 资产

- **几何体**
  - **静态网格体 Static Mesh**：SM_帕斯卡[\_Size]，比如：SM_Rock_Big
  - **骨骼网格体 Skeletal Mesh**：SK_，比如 SK_Hero_Knight
  - **几何体笔刷 Geometry Cache**：GC_，比如 GC_ClothSim
- **材质**
  - **主材质 Material**：M\_, M_Metal_Rust
  - **材质实例 Material Instance**：MI\_，MI_Metal_Gold
  - **材质函数 Material Function**：MF\_，MF_WaveDistortion
  - **材质参数集 Parameter Collection**：MPC_，MPC_GlobalWeather
  - 同一个物体名称有多个材质，可在最后加补全的两位数字（01而不是1）M_MetalBone_01
- **蓝图**
  - **蓝图类 Blueprint Class**，BP\_，BP_Door_Interactive
  - **蓝图接口 Blueprint Interface**：BPI\_，BPI_Damageable
  - **蓝图组件 Actor Component**：BPC\_，BPC_HealthSystem
  - **蓝图函数库 Function Library**：BPL\_，BPL_MathUtils
  - **结构体 Structure**：S\_，S_ItemData
  - **枚举 Enumeration**：E_，E_GameState
  - **输入控制 Input Action**：IA_，IA_Move
- 



## 蓝图

采用帕斯卡命名，将每个单词的首字母大写，不需要连接任何符号或空格

对于**Bool变量**，在首字母前加上小写的b，比如bIsDead，拖动到图里会自动识别为Bool变量
![image-20260129121904357](https://raw.githubusercontent.com/york99alex/Pic4york/main/fix-dir/2026/01/29/74ea41e6f514e343e255bfd9a6524f34-image-20260129121904357-5c59b8.png)







# 链接

## 资源

- [贴图 • Poly Haven](https://polyhaven.com/zh/textures)
- **美术参考图**
  - [ArtStation](https://www.artstation.com/)
  - [Pinterest](https://www.pinterest.com/)
  - [GGAC](https://m.ggac.com/) 国内
- [PBRMAX](https://pbrmax.cn/discover?lan=zh-CN&f=) 国风扫描资产



## 文档

- [虚幻引擎5.6文档 | 虚幻引擎 5.7 文档 | Epic Developer Community](https://dev.epicgames.com/documentation/zh-cn/unreal-engine/unreal-engine-5-7-documentation)
- [UE5材质常用节点笔记](https://zhuanlan.zhihu.com/p/737324219)
- 



## 视频参考

- [【虚幻引擎】爆肝两个月！拜托三连了！这绝对是全B站最用心的UE5.1全中文新手入门公开教程，耗时千余小时开发！_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Cd4y1V7G5/)
  入门4小时+实战4小时
- [MotionDesign 植物生长动画](https://www.bilibili.com/video/BV1Rm42137WL/) Effector使用
- [合集·UE5 C++全面上手  待更新](https://space.bilibili.com/310126275/lists/2910380)
- 



# Demo

目标：多样运动能力，控制物体交互，漂浮固定物体





# TODO

1. 游戏重开逻辑 boss死亡进行重开，通过 lylarboss 获取场景boss，GamePlay
   1. B_TeamDeathMatchScoring 需要响应游戏结束事件清理Timer
   2. 学习掌握 Gameplay Message Subsystem 的发布及订阅方法
   3. 理解Lyra伤害和血量系统
2. 队友伤害硬直  ULyraTeamSubsystem::CanCauseDamage 搜索fixme
3. 射击 修改为 弹道检测（现在是射线检测方案）



# Lyra



## 阶段逻辑整理

1. Boss关卡Map
2. 游戏体验 Gameplay Experience => B_BossArenaExperience 
   可以理解游戏模式的高级版本，从 LyraExperienceDefinition 派生
   1. 依次从 B_BossArenaExperience 中加载 Game Features、Pawn Data、Action Sets、Actions
   2. 在Actions中，Add Abilities、Add Components等
   3. 其中Add Components会为 LyraGameState 挂载若干组件
      1. 其中一个 B_TeamDeathMatchScoring 组件（蓝图类）
         1. 经过主机判断Authority、体验加载ExperienceReady调用方法 StartPhase
            - K2_StartPhase => StartPhase => GiveAbilityAndActivateOnce => InternalTryActivateAbility => CallActivateAbility
         2. 触发 Phase_Warmup 的 Event ActivateAbility
            - 注：所有的 ULyraGamePhaseAbility 的 ActivateAbility 都会调用其 OnBeginPhase，
              而在 OnBeginPhase 中会检测所有 ActivePhases 并 CancelAbilitiesByFunc/OnEndPhase 所有不同级的阶段
         3. Phase_Warmup 加载玩家，全部就位则进入 Phase_Playing
         4. 结束 Phase_Warmup 会触发 B_TeamDeathMatchScoring 在 StartPhase Warmup时委托的事件回调 GameStarted，开启倒计时。
             ==TODO==  修改为累加计时
         5. 倒计时结束触发蓝图内函数 HandleVictory
            1. Activate User Facing Cue 启用 ”MatchDecided” 这一 Gameplay Cue，播放对应特效
            2. 





## Gameplay Message

Gameplay Message Subsystem 提供了高性能、解耦的”发布-订阅“系统