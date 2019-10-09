# school-picker
适用于uni-app开发框架的组件,**全国高校(大学)选择器**

![图片](https://camo.githubusercontent.com/a6798012d98ae0be890a30d5b8c045eecd99b937/68747470733a2f2f696d672e736869656c64732e696f2f6769746875622f6c6963656e73652f4d50436f6d706f6e656e742f6d707675652d636974797069636b65722e737667)

## 组件说明
>基于[mpvue-citypicker](https://github.com/MPComponent/mpvue-citypicker)修改地区部分数据实现

>高校数据来源于[cn-universitysrv](https://github.com/516134941/cn-universitysrv)项目

>GitHub完整文档预览:[school-picker](https://github.com/ATQQ/school-picker)
## 效果
### 只能选择学校

![Snipaste_2019-10-09_08-22-33-2019109](http://img.cdn.sugarat.top/Snipaste_2019-10-09_08-22-33-2019109.png)

![Snipaste_2019-10-09_08-22-46-2019109](http://img.cdn.sugarat.top/Snipaste_2019-10-09_08-22-46-2019109.png)
### 省/市/学校 选其一

![Snipaste_2019-10-09_08-21-53-2019109](http://img.cdn.sugarat.top/Snipaste_2019-10-09_08-21-53-2019109.png)

![Snipaste_2019-10-09_08-20-23-2019109](http://img.cdn.sugarat.top/Snipaste_2019-10-09_08-20-23-2019109.png)

![Snipaste_2019-10-09_08-21-08-2019109](http://img.cdn.sugarat.top/Snipaste_2019-10-09_08-21-08-2019109.png)

### 微信小程序
![schoolPicker-wechat-2019103](http://img.cdn.sugarat.top/schoolPicker-wechat-2019103.gif)

## 简单使用
1. 将components目录下的schoolPicker目录拷贝至所需项目
2. [调用代码](pages/easyDemo/easyDemo.vue)

```vue
<template>
	<view>
		<button type="primary" @click="showSchoolPicker">只选择学校</button>

		<button style="margin-top:1rem;" type="primary" @click="showSchoolPicker2">省/市/学校</button>

		<view style="margin-top: 1rem;text-align: center;">{{schoolData}}</view>
		<!-- 学校选择组件-->
		<schoolPicker themeColor="#000" ref="schoolPicker" @onConfirm="onConfirm">
		</schoolPicker>
		
		<schoolPicker :onlySchool='false' themeColor="#000" ref="schoolPicker2" @onConfirm="onConfirm2">
		</schoolPicker>
		
		<!-- demo 跳转 -->
		<navigator url="../index/index" style="margin-top: 1rem;">
			<button type="default">查看另一demo</button>
		</navigator>
		
	</view>
</template>

<script>
	//高校学校列表组件
	import schoolPicker from '../../components/schoolPicker/schoolPicker.vue';

	export default {
		components: {
			schoolPicker
		},
		data() {
			return {
				schoolData: ''
			}
		},
		methods: {
			/**
			 * 打开学校选择器
			 */
			showSchoolPicker: function() {
				this.$refs.schoolPicker.show()
			},
			/**
			 * 打开 省/市/学校 选择器
			 */
			showSchoolPicker2: function() {
				this.$refs.schoolPicker2.show()
			},
			/**
			 * 确认学校选择
			 */
			onConfirm(e) {
				const school = e.label.split("-")[2];
				console.log(`源数据:${JSON.stringify(e)}`);
				if (school === '暂未收录') {
					return;
				} else {
					this.schoolData = school;
					console.log(`学校:${school}`);
				}
			},
			/**
			 * 确认 省/市/学校 选择
			 */
			onConfirm2(e) {
				this.schoolData = e.label.split("-").reverse().find(v => v != '所有');
			}
		}
	}
</script>
```

## 组件参数
### onlySchool
* 说明:组件是否只能选择学校数据
* 类型:Boolean
* 可选值:true/false
* 是否必填:否
* 默认值:true


### 其他参数
> 参考[mpvue-citypicker](https://github.com/MPComponent/mpvue-citypicker/blob/master/README.md)组件参数
