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
				Roaming
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
						<v-btn outlined rounded text @click="gotolr('page')">
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
						<v-btn outlined rounded text @click="gotoir('page')">
							Learn More
						</v-btn>
					</v-card-actions>
				</v-card>
				<v-card class="mx-auto my-12" width="344" outlined>
					<v-list-item three-line>
						<v-list-item-content>
							<v-list-item-title class="text-h5 mb-4"> Home </v-list-item-title>
							<v-list-item-title class="text-h5 mb-1">300</v-list-item-title>
						</v-list-item-content>

						<v-icon color="Black" large left>mdi-home</v-icon>
					</v-list-item>

					<v-card-actions>
						<v-btn outlined rounded text @click="gotohr('page')">
							Learn More
						</v-btn>
					</v-card-actions>
				</v-card>
			</v-row>
		</div>
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
		</div>
	</v-container>
</template>
<script>
	import { bus } from "C:/Users/Yuvaraj/dashboardnew/src/main.js";

	export default {
		name: "AppPage",

		components: {},

		data: () => ({}),

		methods: {
			gotolr(comp) {
				bus.$emit("switchTolr", comp);
			},
			gotoir(comp) {
				bus.$emit("switchToir", comp);
			},
			gotohr(comp) {
				bus.$emit("switchTohr", comp);
			},
		},
	};
</script>
