<!-- 项目审批明细 -->
<template>
	<view :class="darkMode?'custom-dark':'custom-light'">
		<view class="place-detail">
			<view class="padding-lr padding-tb-xs detail-item">
				<view class="uni-flex uni-row">
					<view class="flex-item-30">审核状态</view>
					<view class="flex-item-70">
						<uni-tag size="small" :text="formatAuditStatus(item.manageStatus).text" :type="formatAuditStatus(item.manageStatus).color"
						 :circle="true"></uni-tag>
					</view>
				</view>
			</view>
			<view class="padding-lr padding-tb-xs detail-item">
				<view class="uni-flex uni-row">
					<view class="flex-item-30">附件</view>
					<view class="flex-item-70">
						<view v-for="atta in item.attachment" :key="atta.url" @tap="filePreview(atta)">
							<uni-icons color="#007aff" type="paperclip" size="22"></uni-icons><text>{{atta.name}}</text>
						</view>
					</view>
				</view>
			</view>
			<view class="padding-lr padding-tb-xs detail-item" v-if="item.opinionList && item.opinionList.length > 0">
				<view class="uni-flex uni-row">
					<view class="uni-timeline">
						<!-- opIndex===0?'uni-timeline-first-item':(opIndex===(item.opinionList.length-1)?'uni-timeline-last-item':'') -->
						<view v-for="(opinion,opIndex) in item.opinionList" :key="opinion.id" class="uni-timeline-item" :class="opIndex===0?'uni-timeline-first-item':(opIndex===(item.opinionList.length-1)?'uni-timeline-last-item':'')">
							<view class="uni-timeline-item-keynode">{{opinion.createTime}}</view>
							<view class="uni-timeline-item-divider"></view>
							<view class="uni-timeline-item-content">
								<view>
									{{`${opinion.examiner}-${opinion.opinion}`}}
								</view>
								<view>
									<uni-tag :inverted="true" size="small" :text="formatAuditStatus(opinion.status).text" :type="formatAuditStatus(opinion.status).color"
									 :circle="false"></uni-tag>
								</view>
							</view>
						</view>
					</view>
				</view>
			</view>
			<view class="cu-bar detail-item solid-bottom">
				<view class="action">
					<text class="cuIcon-title text-blue"></text>项目信息
				</view>
			</view>
			<view class="padding-lr padding-tb-xs detail-item">
				<view class="uni-flex uni-row">
					<view class="flex-item-30">项目名称</view>
					<view class="flex-item-70">{{item.projectName}}</view>
				</view>
			</view>
			<view class="padding-lr padding-tb-xs detail-item">
				<view class="uni-flex uni-row">
					<view class="flex-item-30">项目编号</view>
					<view class="flex-item-70">{{item.projectNo}}</view>
				</view>
			</view>
			<view class="padding-lr padding-tb-xs detail-item">
				<view class="uni-flex uni-row">
					<view class="flex-item-30">项目类别</view>
					<view class="flex-item-70">{{item.projectType}}</view>
				</view>
			</view>
			<view class="padding-lr padding-tb-xs detail-item">
				<view class="uni-flex uni-row">
					<view class="flex-item-30">项目区域</view>
					<view class="flex-item-70">{{item.area}}</view>
				</view>
			</view>

			<view class="cu-bar detail-item solid-bottom">
				<view class="action">
					<text class="cuIcon-title text-blue"></text>立项信息
				</view>
			</view>
			<view class="padding-lr padding-tb-xs detail-item">
				<view class="uni-flex uni-row">
					<view class="flex-item-30">立项人</view>
					<view class="flex-item-70">{{item.createUser}}</view>
				</view>
			</view>
			<view class="padding-lr padding-tb-xs detail-item">
				<view class="uni-flex uni-row">
					<view class="flex-item-30">立项时间</view>
					<view class="flex-item-70">{{item.createTime}}</view>
				</view>
			</view>
			<view class="padding-lr padding-tb-xs detail-item">
				<view class="uni-flex uni-row">
					<view class="flex-item-30">预计开始时间</view>
					<view class="flex-item-70">{{item.startTime}}</view>
				</view>
			</view>
			<view class="padding-lr padding-tb-xs detail-item">
				<view class="uni-flex uni-row">
					<view class="flex-item-30">预计结束时间</view>
					<view class="flex-item-70">{{item.endTime}}</view>
				</view>
			</view>

			<view class="cu-bar detail-item solid-bottom">
				<view class="action">
					<text class="cuIcon-title text-blue"></text>其他信息
				</view>
			</view>
			<view class="padding-lr padding-tb-xs detail-item">
				<view class="uni-flex uni-row">
					<view class="flex-item-30">业主单位</view>
					<view class="flex-item-70">{{item.ownerUnit}}</view>
				</view>
			</view>
			<view class="padding-lr padding-tb-xs detail-item">
				<view class="uni-flex uni-row">
					<view class="flex-item-30">建设单位</view>
					<view class="flex-item-70">{{item.buildUnit}}</view>
				</view>
			</view>
			<view class="padding-lr padding-tb-xs detail-item">
				<view class="uni-flex uni-row">
					<view class="flex-item-30">项目紧急程度</view>
					<view class="flex-item-70">{{item.agencyDegree}}</view>
				</view>
			</view>
			<view class="padding-lr padding-tb-xs detail-item">
				<view class="uni-flex uni-row">
					<view class="flex-item-30">人力投入情况</view>
					<view class="flex-item-70">{{item.human}}</view>
				</view>
			</view>
			<view class="padding-lr padding-tb-xs detail-item">
				<view class="uni-flex uni-row">
					<view class="flex-item-30">甲方资金来源</view>
					<view class="flex-item-70">{{item.aFoundSource}}</view>
				</view>
			</view>
			<view class="padding-lr padding-tb-xs detail-item">
				<view class="uni-flex uni-row">
					<view class="flex-item-30">项目描述</view>
					<view class="flex-item-70">{{item.descript}}</view>
				</view>
			</view>
		</view>
		<view class="goods-carts">
			<uni-goods-nav :options="options" :button-group="buttonGroup" @click="onClick" @buttonClick="buttonClick" />
		</view>
		<audit-idea ref="popupAuditIdeaRef" :isPass="isPass" @updateQuery="updateQuery"></audit-idea>
	</view>
</template>

<script>
	import { mapGetters } from 'vuex'
	import uniGoodsNav from '@/components/uni-goods-nav/uni-goods-nav.vue'
	import uniTag from '@/components/uni-tag/uni-tag.vue'
	import uniIcons from '@/components/uni-icons/uni-icons.vue'
	import auditIdea from '@/pages/index/audit-idea.vue'
	import {
		filePreview,
		formatAuditStatus
	} from '@/utils/index.js'
	export default {
		components: {
			uniGoodsNav,
			uniTag,
			uniIcons,
			auditIdea
		},
		computed: {
			...mapGetters(['themeBgColor', 'darkMode']),
		},
		data() {
			return {
				isPass: false,
				item: {},
				options: [{
					icon: '/static/img/edit.png',
					text: '调整'
				}],
				buttonGroup: [{
						text: '拒绝',
						backgroundColor: '#e54d42',
						color: '#fff'
					},
					{
						text: '通过',
						backgroundColor: '#39b54a',
						color: '#fff'
					}
				]
			}
		},
		onReady() {
			uni.setNavigationBarTitle({
			    title: this.$t('ProjectApproval')
			})
			// navBar-bg-color
			uni.setNavigationBarColor({
			    frontColor: '#ffffff',
			    backgroundColor: this.themeBgColor,
			    animation: {
			        duration: 400,
			        timingFunc: 'easeIn'
			    }
			})
		},
		onLoad(options) {
			try {
				this.item = JSON.parse(options.data)
			} catch (e) {
				this.item = []
			}
		},
		methods: {
			filePreview,
			formatAuditStatus,
			onClick(e) {
				// uni.showToast({
				// 	title: `点击${e.content.text}`,
				// 	icon: 'none'
				// })
				if (e.content.text === '调整') {
					uni.navigateTo({
						url: '/pages/index/project/adjust-project?data=' + JSON.stringify(this.item)
					})
				}
			},
			buttonClick(e) {
				if (e.index === 0) {
					this.isPass = false
					this.$refs.popupAuditIdeaRef.$refs.share.open()
				} else if (e.index === 1) {
					this.isPass = true
					this.$refs.popupAuditIdeaRef.$refs.share.open()
				}
			},
			updateQuery() {
				// 更新数据
				let pages = getCurrentPages()
				// let currPage = pages[pages.length - 1]; //当前页面
				let prevPage = pages[pages.length - 2] //上一个页面
				prevPage.isDoRefresh = true
				setTimeout(() => {
					uni.navigateBack({
						delta: 1
					})
				}, 1000)
			}
		}
	}
</script>

<style>
	.place-detail {
		/* margin: 27rpx 20rpx 104rpx 20rpx; */
		padding-bottom: 104rpx;
	}

	/* .place-detail .uni-row {
		margin: 5rpx 0;
	} */
</style>
