<template>
	<div id="app">

		<div class="content" v-loading="loading">
			<div id="container"></div>
			<router-view v-if="!microAppsActive" />
		</div>
	</div>
</template>

<script>
	import {
		registerMicroApps,
		start
	} from '@ice/stark';
	import {
		setBasename
	} from '@ice/stark-app';
	import Layout from './layouts/BasicLayout'

	export default {
		data() {
			return {
				loading: false,
				microAppsActive: false,
			}
		},
		name: 'App',
		components: {
			Layout,
		},
		mounted() {
			const container = document.getElementById('container');
			registerMicroApps([{
				name: 'njkt',
				activePath: '/njkt',
				title: '商家平台',
				sandbox: true,
				// React app demo: https://github.com/alibaba-fusion/materials/tree/master/scaffolds/ice-stark-child
				url: [
					// 'http:////acechinese.cn/dist/js/app.js',
					// 'http:////acechinese.cn/dist/js/home.js',
					// 'http:////acechinese.cn/dist/js/activity.js',
					// 'http:////acechinese.cn/dist/js/expert.js',
					// 'http:////acechinese.cn/dist/js/myExperts.js',
					// 'http:////acechinese.cn/dist/js/myArticles.js',
					// 'http:////acechinese.cn/dist/js/myCourses.js',
					// 'http:////acechinese.cn/dist/js/expertDetail.js',
					// 'http:////acechinese.cn/dist/js/live.js',
					// 'http:////acechinese.cn/dist/js/help.js',
					// 'http:////acechinese.cn/dist/js/article.js',
					// 'http:////acechinese.cn/dist/js/course.js',
					// 'http:////acechinese.cn/dist/css/app.css',
					// 'http:////acechinese.cn/dist/css/home.css',
					// 'http:////acechinese.cn/dist/css/myExperts.css',
					// 'http:////acechinese.cn/dist/css/myExperts.css',
					// 'http:////acechinese.cn/dist/css/myCourses.css',
					// 'http:////acechinese.cn/dist/css/expertDetail.css',
					// 'http:////acechinese.cn/dist/css/activity.css',
					// 'http:////acechinese.cn/dist/css/article.css',
					// 'http:////acechinese.cn/dist/css/course.css',
					// 'http:////acechinese.cn/dist/css/expert.css',
					// 'http:////acechinese.cn/dist/css/help.css',
					// 'http:////acechinese.cn/dist/css/live.css',
					'http:////localhost/dist/js/app.js',
					'http:////localhost/dist/js/home.js',
					'http:////localhost/dist/js/activity.js',
					'http:////localhost/dist/js/expert.js',
					'http:////localhost/dist/js/myExperts.js',
					'http:////localhost/dist/js/myArticles.js',
					'http:////localhost/dist/js/myCourses.js',
					'http:////localhost/dist/js/expertDetail.js',
					'http:////localhost/dist/js/live.js',
					'http:////localhost/dist/js/myMsgs.js',
					'http:////localhost/dist/js/help.js',
					'http:////localhost/dist/js/article.js',
					'http:////localhost/dist/js/course.js',
					'http:////localhost/dist/css/app.css',
					'http:////localhost/dist/css/home.css',
					'http:////localhost/dist/css/myExperts.css',
					'http:////localhost/dist/css/myExperts.css',
					'http:////localhost/dist/css/myCourses.css',
					'http:////localhost/dist/css/expertDetail.css',
					'http:////localhost/dist/css/activity.css',
					'http:////localhost/dist/css/article.css',
					'http:////localhost/dist/css/course.css',
					'http:////localhost/dist/css/expert.css',
					'http:////localhost/dist/css/help.css',
					'http:////localhost/dist/css/live.css',
					'http:////localhost/dist/css/myMsgs.css',
				],
				container,
			}, ]);

			start({
				onAppEnter: (appConfig) => {
					const {
						activePath
					} = appConfig;
					setBasename(activePath)
				},
				onLoadingApp: () => {
					this.loading = true;
				},
				onFinishLoading: () => {
					this.loading = false;
				},
				onRouteChange: (_, pathname) => {
					// 处理微应用间跳转无法触发 Vue Router 响应
					this
						.$router
						.push(pathname)
						.catch(() => {})
				},
				onActiveApps: (activeApps) => {
					this.microAppsActive = (activeApps || []).length;
				}
			});
		},
	}
</script>

<style>
	#app {
		font-family: Avenir, Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		color: #2c3e50;
		height: 100vh;

		display: flex;
	}

	body {
		margin: 0;
		padding: 0;
	}

	.content {
		flex: 1;
		margin: 40px;
	}

	.el-rwo {
		height: 100%;
	}
</style>
