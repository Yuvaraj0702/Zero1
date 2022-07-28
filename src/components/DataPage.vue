<template>
	<v-container>
		<div>
			<div
				class="text-h3 mb-16"
				style="
					padding-top: 0px;
					padding-right: 20px;
					padding-bottom: 0px;
					padding-left: 20px;
				"
			>
				<br />
				Data
			</div>
			<v-row>
				<v-card class="mx-auto my-12" width="344" outlined>
					<v-list-item three-line>
						<v-list-item-content>
							<v-list-item-title class="text-h5 mb-4">
								Local
							</v-list-item-title>
							<v-list-item-title class="text-h5 mb-1">300</v-list-item-title>
						</v-list-item-content>

						<v-icon color="Black" large left>mdi-map-marker-radius</v-icon>
					</v-list-item>

					<v-card-actions>
						<v-btn outlined rounded text @click="gotoLocalD('page')">
							Learn More
						</v-btn>
					</v-card-actions>
				</v-card>
				<v-card class="mx-auto my-12" width="344" outlined>
					<v-list-item three-line>
						<v-list-item-content>
							<v-list-item-title class="text-h5 mb-4">
								International
							</v-list-item-title>
							<v-list-item-title class="text-h5 mb-1">150</v-list-item-title>
						</v-list-item-content>

						<v-icon color="Black" large left>mdi-web</v-icon>
					</v-list-item>

					<v-card-actions>
						<v-btn outlined rounded text @click="gotoIntD('page')">
							Learn More
						</v-btn>
					</v-card-actions>
				</v-card>
			</v-row>
		</div>
	</v-container>
</template>
<script>
	import { bus } from "../main.js";
	export default {
		name: "AppPage",

		components: {},

		data: () => ({
			// component: LoginPage,
		}),
		//   created() {
		//     bus.$on("switchToMain", () => {
		//       this.component = MainPage;
		//     });
		//       bus.$on("switchToLogin", () => {
		//       this.component = LoginPage;
		//     });
		//   },
		methods: {
			gotoLocalD(comp) {
				bus.$emit("switchToLocalD", comp);
			},
			gotoIntD(comp) {
				bus.$emit("switchToIntD", comp);
			},
		},
	};
</script>
