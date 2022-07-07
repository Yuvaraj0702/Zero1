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
				],
			};
		},
		mounted(){
				fetch("/api/v1/IDD").then((response) =>response.json()).then((data) => {this.desserts=data;})
		}

	};
</script>
