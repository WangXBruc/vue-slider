# vue-slider-component
an image slider component with Vue

### 实现一组图片无限循环轮播的原理是：

共有三级节点，最外层的节点固定，是展示给用户看到的部分；

第二层是包含图片组的容器；

第三层是图片组，**这里需要复制一份完全相同的轮播图片组**。

![slider](https://github.com/WangXBruc/vue-slider-component/blob/master/slider.png)

图片逐步向左移动，当demo中的四张图片全部移出到页面左侧时，**立刻把图片恢复到初始化的位置，循环往复**。

### 需要注意的事项

鼠标移入时重新执行动画，移出时再次开始执行动画。我们需要的效果是图片始终匀速移动，因此在 animate函数中**执行时间需要在保持移动速度不变的情况下，动态设置。**



