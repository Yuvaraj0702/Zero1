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
				Home Roaming
			</div>
			<v-data-table
				:headers="headers"
				:items="desserts"
				:items-per-page="5"
				class="elevation-1"
				style="
					padding-top: 0px;
					padding-right: 20px;
					padding-bottom: 20px;
					padding-left: 20px;
				"
			></v-data-table>
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
		<v-row class="flex-nowrap">
			<v-spacer></v-spacer>
			<v-btn @click="gotoroam('page')"> Back to Roaming </v-btn>
		</v-row>
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
		data() {
			return {
				headers: [
					{
						text: "Destination Country",
						align: "start",
						sortable: false,
						value: "name",
					},

					{ text: "Billing cycle", value: "calories" },
					{ text: "Phone number", value: "calories" },
					{ text: "ID Type", value: "calories" },
					{ text: "Mins called", value: "calories" },
					{ text: "Mins called from plan 1", value: "fat" },
					{ text: "Mins called from plan 2", value: "carbs" },
					{ text: "Mins called from plan 3", value: "protein" },
				],
				desserts: [
					{
						name: "Argentina",
						calories: 159,
						fat: 6.0,
						carbs: 24,
						protein: 4.0,
						iron: "1%",
					},
					{
						name: "Brunei",
						calories: 237,
						fat: 9.0,
						carbs: 37,
						protein: 4.3,
						iron: "1%",
					},
					{
						name: "China",
						calories: 262,
						fat: 16.0,
						carbs: 23,
						protein: 6.0,
						iron: "7%",
					},
					{
						name: "India",
						calories: 305,
						fat: 3.7,
						carbs: 67,
						protein: 4.3,
						iron: "8%",
					},
					{
						name: "Uganda",
						calories: 356,
						fat: 16.0,
						carbs: 49,
						protein: 3.9,
						iron: "16%",
					},
					{
						name: "Yemen",
						calories: 375,
						fat: 0.0,
						carbs: 94,
						protein: 0.0,
						iron: "0%",
					},
				],
			};
		},
		methods: {
			gotoroam(comp) {
				bus.$emit("switchToRoam", comp);
			},
		},
	};
</script>
