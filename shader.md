baseVertexShader - 基础顶点着色器。
blurVertexShader - 模糊效果的顶点着色器。
blurShader - 模糊效果的片段着色器。
copyShader - 复制操作的着色器。
clearShader - 清除操作的着色器。
colorShader - 颜色应用的着色器。
checkerboardShader - 棋盘图案的着色器。
displayShaderSource - 显示操作的着色器源代码。
bloomPrefilterShader - 光晕效果预过滤的着色器。
bloomBlurShader - 光晕效果模糊的着色器。
bloomFinalShader - 光晕效果最终的着色器。
sunraysMaskShader - 阳光效果的遮罩着色器。
sunraysShader - 阳光效果的着色器。
splatShader - 溅射效果的着色器。
advectionShader - 对流效果的着色器。
divergenceShader - 发散效果的着色器。
curlShader - 卷曲效果的着色器。
vorticityShader - 涡旋效果的着色器。
pressureShader - 压力计算的着色器。
gradientSubtractShader - 梯度减法操作的着色器。



这些着色器在 WebGL 流体仿真中各自扮演不同的角色，并通过协同工作来实现复杂的视觉效果和物理仿真。以下是它们如何协同工作的概述：
1. **顶点着色器（Vertex Shaders）**：
   - `baseVertexShader` 和 `blurVertexShader`：这些着色器处理顶点数据的变换，如位置和纹理坐标。它们为片段着色器提供输入数据。
2. **片段着色器（Fragment Shaders）**：
   - `blurShader`、`copyShader`、`clearShader`、`colorShader`、`checkerboardShader`、`bloomPrefilterShader`、`bloomBlurShader`、`bloomFinalShader`、`sunraysMaskShader`、`sunraysShader`、`splatShader`、`advectionShader`、`divergenceShader`、`curlShader`、`vorticityShader`、`pressureShader`、`gradientSubtractShader`：这些着色器负责计算像素颜色，实现各种视觉效果，如模糊、颜色应用、光晕、阳光、溅射、对流、发散、卷曲、涡旋、压力计算和梯度减法。
3. **仿真流程**：
   - **初始化**：设置画布、WebGL 上下文、纹理和帧缓冲区。
   - **用户输入**：通过 `splatShader` 将用户输入（如鼠标点击）转换为流体仿真中的溅射效果。
   - **对流**：`advectionShader` 用于模拟流体的对流效果，根据速度场移动流体。
   - **速度场处理**：
     - `divergenceShader` 计算速度场的发散。
     - `curlShader` 计算速度场的卷曲。
     - `vorticityShader` 增强流体的涡旋效果。
   - **压力求解**：`pressureShader` 和 `gradientSubtractShader` 用于求解压力场，确保流体仿真符合不可压缩流体的条件。
   - **视觉效果**：
     - `blurShader` 和 `bloom*Shaders` 用于实现光晕效果。
     - `sunraysMaskShader` 和 `sunraysShader` 用于模拟阳光穿透效果。
     - `checkerboardShader` 用于在流体不覆盖的区域显示棋盘图案。
   - **渲染输出**：最终，通过 `displayShaderSource` 将仿真结果渲染到屏幕上。
4. **协同工作**：
   - 着色器程序通过 WebGL 的渲染管线协同工作。顶点着色器处理几何形状，片段着色器处理像素颜色。
   - 着色器之间通过纹理和帧缓冲区交换数据。例如，一个着色器的输出可以作为另一个着色器的输入纹理。
   - 通过多次渲染迭代和不同的着色器组合，实现复杂的视觉效果和物理仿真。
5. **性能优化**：
   - 使用多重渲染目标（MRT）和帧缓冲区对象（FBO）来减少渲染次数和提高性能。
   - 通过调整着色器参数和仿真分辨率来平衡视觉效果和性能。
这些着色器通过精心设计的渲染流程和数据处理流程，共同构成了一个完整的流体仿真系统，实现了实时、交互式的流体动力学仿真和视觉效果。
