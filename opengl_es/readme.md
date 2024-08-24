# opengl 有什么用？
可以绘制一些3D效果，
复杂的图片特效

# Android上如何开发opengl
https://github.com/githubhaohao/NDK_OpenGLES_3_0
- 利用opengl es提供的api进行指定效果的开发
- 需要用到jni
app
->cpp
  ->client.cpp头文件
  ->CMakeLists.txt cmake编译文件
->java
->jniLibs cpp编译需要引入的so
* 需要将opengl相关的头文件以及so引入工程
* 哪些是开发opengl需要引入的头文件以及so

* glm是什么 
> GLM 是 OpenGL Mathematics 的缩写，它是一个用于图形编程的数学库。  
> GLM 提供了一组数学工具和函数，这些工具和函数主要用于处理图形编程中的线性代数操作，如矩阵变换、向量运算和四元数操作等        
* inc/assimp
> 在OpenGL中，Assimp（Open Asset Import Library）是一个库，用于导入各种3D模型文件格式。它提供了一个统一的接口，支持多种不同的文件格式，如 OBJ、FBX、3DS 和 COLLADA 等，使得从各种格式中加载3D模型变得更加简单。通过使用 Assimp，开发者可以轻松地解析和处理模型数据，获取顶点、法线、纹理坐标等信息，并将这些数据用于OpenGL渲染
* inc/freetype_2_9_1
> FreeType 是一个开源库，用于处理和渲染字体       
> FreeType 提供了对各种字体格式的支持，包括 TrueType 和 OpenType 字体。        
* opencv_3_0_0
> 是一个跨平台的计算机视觉库      

使用了两个方式实现了native和java
https://blog.csdn.net/afei__/article/details/84821570


参考连接：
https://www.rtcdeveloper.cn/cn/community/blog/21656
https://www.khronos.org/opengles/





