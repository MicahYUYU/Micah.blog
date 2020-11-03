title: Element UI
author: Micah
date: 2020-05-07 11:58:57
tags:

---

##### Element UI 默认样式修改的问题

当我们在 vue 中引入第三方组件库的时候，vue 组件中样式的 scoped 就会成为我们修改样式的阻碍，有以下三种方法修改样式，并且不影响全局样式：

1. 在样式外新增一个样式不添加 scoped

```scss
<style>
	.my{
		margin: 20px;
	}
	.my .el-input__inner{
		border-radius: 15px;/* 这个样式起效果 */
	}
</style>
<style scoped>
	.my .el-input__inner{
		border-radius: 30px; /* 这个样式不起效果 */
	}
</style>
```

2. 使用 deep 样式穿透

```scss
<style scoped>
	.my .el-input__inner{
		border-radius: 30px;/* 这个不起作用 */
	}
	.my /deep/ .el-input__inner{
		border-radius: 30px;/* 这个起作用 */
	}
</style>
```

3. 使用>>>穿透  
   不晓得为啥有的时候这种方式穿透不了

```scss
<style scoped>
	.my .el-input__inner{
		border-radius: 30px;/* 这个不起作用 */
	}
	.my >>> .el-input__inner{
		border-radius: 30px;/* 这些起作用 */
		border: 1px solid #eceef2;
		outline: 0;
	}
</style>
```

4. 有些样式是行内样式权重比较高则需要使用上面的几种方法来保证可以修改样式并且添加上!important 来增加权重

```scss
<el-input v-model="input" placeholder="请输入内容" style="width: 300px;"></el-input>
<style scoped>
	.my >>> .el-input__inner{
		border-radius: 30px;
		border: 1px solid #eceef2;
		outline: 0;
		width: 400px!important;
	}
</style>
```
