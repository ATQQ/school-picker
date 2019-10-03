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
