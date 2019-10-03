# school-picker
适用于uni-app开发框架的组件,**全国高校(大学)选择器**

![](https://camo.githubusercontent.com/a6798012d98ae0be890a30d5b8c045eecd99b937/68747470733a2f2f696d672e736869656c64732e696f2f6769746875622f6c6963656e73652f4d50436f6d706f6e656e742f6d707675652d636974797069636b65722e737667)
## 组件说明
>基于[mpvue-citypicker](https://github.com/MPComponent/mpvue-citypicker)修改地区部分数据实现

>高校数据来源于[cn-universitysrv](https://github.com/516134941/cn-universitysrv)项目

## 效果
### 微信小程序

![](static/schoolPicker-wechat.gif)

### Android

![](static/school-picker-android.jpg)

## 简单使用
1. 克隆此仓库到本地,将components目录下的schoolPicker目录拷贝至所需项目
2. [调用代码](pages/easyDemo/easyDemo.vue)
```vue
<template>
	<view >
		<button type="primary" @click="showSchoolPicker">点击选择学校</button>
		<text>{{schoolData}}</text>
		<!-- 学校选择组件-->
		<schoolPicker themeColor="#000" ref="schoolPicker"
		 @onConfirm="onConfirm">
		</schoolPicker>
	</view>
</template>

<script>
	//高校学校列表组件
	import schoolPicker from '../../components/schoolPicker/schoolPicker.vue'; 
	
	export default {
		components:{
			schoolPicker
		},
		data(){
			return{
				schoolData:''
			}
		},
		methods: {
			/**
			 * 打开学校选择器
			 */
			showSchoolPicker:function(){
				this.$refs.schoolPicker.show()
			},
			/**
			 * 确认选择
			 */
			onConfirm(e) {
				const school = e.label.split("-")[2];
				console.log(`源数据:${JSON.stringify(e)}`);
				if (school === '暂未收录') {
					return;
				} else {
					this.schoolData=school;
					console.log(`学校:${school}`);
				}
			}
		}
	}
</script>
```

## 组件参数
> 参考[mpvue-citypicker](https://github.com/MPComponent/mpvue-citypicker/blob/master/README.md)组件参数
