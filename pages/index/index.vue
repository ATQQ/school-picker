<template>
	<view class="content">
		<view class="text-area">
			<text class="title">{{title}}</text>
		</view>
		<view class="content-item">
			<textarea :value="jsonData" placeholder="显示回调的json数据"/>
		</view>
		<view class="content-item">
			<input :value="schoolData" placeholder="此处显示选择的学校"/>
		</view>
		<view class="content-item">
			<button type="primary" @click="showSchoolPicker">只选择学校</button>
		</view>
		<view class="content-item">
			<button type="primary" @click="showSchoolPicker2">选择省/市/大学</button>
		</view>
		
		<!-- 学校选择组件(支持 全国与所有 选项)-->
		<schoolPicker :onlySchool='false' themeColor="#000" ref="schoolPicker2" :pickerValueDefault="cityPickerValueDefault"
		 @onConfirm="onConfirm2">
		</schoolPicker>
		
		<!-- 学校选择组件-->
		<schoolPicker themeColor="#000" ref="schoolPicker" :pickerValueDefault="cityPickerValueDefault"
		 @onConfirm="onConfirm">
		</schoolPicker>
	</view>
</template>

<script>
	import schoolPicker from '../../components/schoolPicker/schoolPicker.vue'; //学校列表插件
	
	
	export default {
		data() {
			return {
				title: 'school-picker演示demo',
				jsonData:'',//json数据
				schoolData:'',//学校数据
				cityPickerValueDefault: [0, 0, 0],
			}
		},
		components:{
			schoolPicker
		},
		methods: {
			/**
			 * 打开学校选择器
			 */
			showSchoolPicker:function(){
				this.$refs.schoolPicker.show()
			},
			showSchoolPicker2:function(){
				this.$refs.schoolPicker2.show()
			},
			/**
			 * 只选择学校的 确认选择
			 */
			onConfirm(e) {
				const school = e.label.split("-")[2];
				if (school === '暂未收录') {
					return;
				} else {
					this.schoolData = school;
					this.jsonData=JSON.stringify(e);
				}
			},
			/**
			 * 省/市/大学 确认选择
			 */
			onConfirm2(e) {
				let result = (e.label.split("-")).reverse();
				result=result.find(v=>{
					return v!=='所有';
				})
				this.schoolData = result;
				this.jsonData=JSON.stringify(e);
			}
		}
	}
</script>

<style>
	.content-item{
		text-align: center;
		margin-top: 1rem;
	}
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.text-area {
		margin-top: 2rem;
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 1rem;
		color: #8f8f94;
	}
</style>
