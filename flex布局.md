# flex布局

~~~ js
//可以对行内元素设置宽度，默认从左到右排序(不需要浮动)
// 可以直接加margin:auto ,就可以水平居中

// 改变主轴方向
flex-direction:row; // 默认值  主轴为x轴 1-2-3-4-5
flex-direction:column; // 主轴为y轴 竖着排列

// 主轴的反向排列
flex-direction:row-reverse;   // 5-4-3-2-1
flex-direction:columun-reverse;  // 得先把主轴设置为y轴才好使，flex-direction:column;

// 默认从左到右，从上到下对齐，改变对其方式 
just-content: flex-end;  // 从右到左，从下到上对齐
just-content: flex-end;   // 默认值 从左到右，从上到下对齐
just-content: center;   // 居中对齐
just-content: space-between;  // 左右靠边对其 ，中间自动分配
just-content: space-around;   // 父元素里的子元素，平局分配父元素剩下的距离

// 改变侧轴的方向
display:flex;
flex-direction:column;
align-items:flex-end;   // 竖者，右对齐
align-items:center;    // 竖着，中间对齐

// 弹性盒子子元素换行问题 都是添加在父元素上，不添加就会一直在一行显示
display: flex;
flex-wrap:wrap; // 换行，等距离平分
flex-wrap:no-wrap; // 默认值不换行
flex-wrap:wrap-reverse; // 子元素在夫元素里面反向换行

// 行与行之间的对齐方式 添加在父元素上
align-content:flex-start;  //没有了行间距
align-content:flex-end;   // 子元素在父元素底部对齐，没有了行间距
align-content:center; 	// 
align-content:space-between; // 子元素在父元素里，两端对齐，中间自动分配
align-content:space-around;   // 子元素在父元素里行间距自动分配

// 控制在侧轴上的对齐方式  *添加在子元素上的属性
align-self:auto;		// 默认值
algn-self:center;		// 子元素位于测轴的方向居中
align-self:flex-start;  // 子元素位于容器的开头
align-self:flex-start;  // 子元素位于容器的结尾

// 拉伸
align-self:stretch;  // 不给高度的话，会拉伸充满父元素 *添加在子元素上的属性

// 排序 *添加在子元素上的属性
order:           // 谁的数字越小谁越靠前


// 自动分配
flex:1;   // 把剩余的空间给他
// 如果子元素都加flex:1 都平均分配

~~~



