<template>
	<v-app id="div1">
		<component v-bind:is="component" />
	</v-app>
</template>

<script>
	import { bus } from "C:/Users/Yuvaraj/dashboardnew/src/main.js";
	import LoginPage from "C:/Users/Yuvaraj/dashboardnew/src/components/LoginPage.vue";
	import MainPage from "C:/Users/Yuvaraj/dashboardnew/src/components/MainPage.vue";

	export default {
		name: "AppPage",

		components: {
			MainPage,
			LoginPage,
		},

		data: () => ({
			component: MainPage,
		}),
		created() {
			bus.$on("switchToMain", () => {
				this.component = MainPage;
			});
			//   bus.$on("switchToLogin", () => {
			//   this.component = LoginPage;
			// });
		},
	};
</script>
<style scoped>
	#div1 {
		background-color: red;
	}
</style>
