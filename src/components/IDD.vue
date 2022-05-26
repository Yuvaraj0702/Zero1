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
				IDD
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
	</v-container>
</template>
<script>
	export default {
		data() {
			return {
				headers: [
					{
						text: "Destination Country",
						align: "start",
						sortable: false,
						value: "destination_country",
					},
					{ text: "Mins called", value: "id" },
					{ text: "Mins called from plan 1", value: "mincCalled1" },
					{ text: "Mins called from plan 2", value: "mincCalled2" },
					{ text: "Mins called from plan 3", value: "mincCalled3" },
				],
				desserts: [
					// {
					// 	name: "Argentina",
					// 	calories: 159,
					// 	fat: 6.0,
					// 	carbs: 24,
					// 	protein: 4.0,
					// 	iron: "1%",
					// },
					// {
					// 	name: "Brunei",
					// 	calories: 237,
					// 	fat: 9.0,
					// 	carbs: 37,
					// 	protein: 4.3,
					// 	iron: "1%",
					// },
					// {
					// 	name: "China",
					// 	calories: 262,
					// 	fat: 16.0,
					// 	carbs: 23,
					// 	protein: 6.0,
					// 	iron: "7%",
					// },
					// {
					// 	name: "India",
					// 	calories: 305,
					// 	fat: 3.7,
					// 	carbs: 67,
					// 	protein: 4.3,
					// 	iron: "8%",
					// },
					// {
					// 	name: "Uganda",
					// 	calories: 356,
					// 	fat: 16.0,
					// 	carbs: 49,
					// 	protein: 3.9,
					// 	iron: "16%",
					// },
					// {
					// 	name: "Yemen",
					// 	calories: 375,
					// 	fat: 0.0,
					// 	carbs: 94,
					// 	protein: 0.0,
					// 	iron: "0%",
					// },
				],
			};
		},
		mounted(){
				fetch("/api/v1/IDD").then((response) =>response.json()).then((data) => {this.desserts=data;}).then(console.log(this.desserts))
		}

	};
</script>
