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
				Voice
			</div>
			<v-row>
				<v-card class="mx-auto my-12" width="344" outlined>
					<v-list-item three-line>
						<v-list-item-content>
							<v-list-item-title class="text-h5 mb-4">
								Outgoing
							</v-list-item-title>
							<v-list-item-title class="text-h5 mb-1">300</v-list-item-title>
						</v-list-item-content>

						<v-icon color="Black" large left>mdi-phone-outgoing</v-icon>
					</v-list-item>

					<v-card-actions>
						<v-btn outlined rounded text @click="gotoout('page')">
							Learn More
						</v-btn>
					</v-card-actions>
				</v-card>
				<v-card class="mx-auto my-12" width="344" outlined>
					<v-list-item three-line>
						<v-list-item-content>
							<v-list-item-title class="text-h5 mb-4">
								Incoming
							</v-list-item-title>
							<v-list-item-title class="text-h5 mb-1">150</v-list-item-title>
						</v-list-item-content>

						<v-icon color="Black" large left>mdi-phone-incoming</v-icon>
					</v-list-item>

					<v-card-actions>
						<v-btn outlined rounded text @click="gotoinc('page')">
							Learn More
						</v-btn>
					</v-card-actions>
				</v-card>
				<v-card class="mx-auto my-12" width="344" outlined>
					<v-list-item three-line>
						<v-list-item-content>
							<v-list-item-title class="text-h5 mb-4"> IDD </v-list-item-title>
							<v-list-item-title class="text-h5 mb-1">300</v-list-item-title>
						</v-list-item-content>

						<v-icon color="Black" large left>mdi-waves</v-icon>
					</v-list-item>

					<v-card-actions>
						<v-btn outlined rounded text @click="gotoidd('page')">
							Learn More
						</v-btn>
					</v-card-actions>
				</v-card>
			</v-row>
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
			gotoout(comp) {
				bus.$emit("switchToOutGraph", comp);
			},
			gotoinc(comp) {
				bus.$emit("switchToIncGraph", comp);
			},
			gotoidd(comp) {
				bus.$emit("switchToIDD", comp);
			},
		},
	};
</script>
