<template>
	<v-container>
		<div>
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
					Local SMS By Month
				</div>
				<LineChartGenerator
					:chart-options="chartOptions"
					:chart-data="chartData"
					:chart-id="chartId"
					:dataset-id-key="datasetIdKey"
					:plugins="plugins"
					:css-classes="cssClasses"
					:styles="styles"
					:width="width"
					:height="height"
				/>
			</div>
			<div
				style="
					padding-top: 45px;
					padding-right: 20px;
					padding-bottom: 0px;
					padding-left: 20px;
				"
			>
				<v-row class="flex-nowrap">
					<v-spacer></v-spacer>
					<v-btn @click="ldy('page')"> By Year </v-btn>
					<v-spacer></v-spacer>
					<v-btn @click="ldm('page')"> By Month </v-btn>
					<v-spacer></v-spacer>
					<v-btn @click="ldd('page')"> By Day </v-btn>
					<v-spacer></v-spacer>
					<v-btn @click="ldh('page')"> By Hour </v-btn>
					<v-spacer></v-spacer>
					<v-btn @click="gotoSMS('page')"> Back To SMS </v-btn>
					<v-spacer></v-spacer>
				</v-row>
			</div>
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
	import { Line as LineChartGenerator } from "vue-chartjs/legacy";
	import { bus } from "C:/Users/Yuvaraj/dashboardnew/src/main.js";

	import {
		Chart as ChartJS,
		Title,
		Tooltip,
		Legend,
		LineElement,
		LinearScale,
		CategoryScale,
		PointElement,
	} from "chart.js";

	ChartJS.register(
		Title,
		Tooltip,
		Legend,
		LineElement,
		LinearScale,
		CategoryScale,
		PointElement
	);

	export default {
		name: "LineChart",
		components: {
			LineChartGenerator,
		},
		props: {
			chartId: {
				type: String,
				default: "line-chart",
			},
			datasetIdKey: {
				type: String,
				default: "label",
			},
			width: {
				type: Number,
				default: 400,
			},
			height: {
				type: Number,
				default: 400,
			},
			cssClasses: {
				default: "",
				type: String,
			},
			styles: {
				type: Object,
				default: () => {},
			},
			plugins: {
				type: Array,
				default: () => [],
			},
		},
		data() {
			return {
				chartData: {
					labels: [
						"January",
						"February",
						"March",
						"April",
						"May",
						"June",
						"July",
						"August",
						"September",
						"October",
						"November",
						"December",
					],
					datasets: [
						{
							label: "Data",
							backgroundColor: "red",
							data: [],
						},
					],
				},
				chartOptions: {
					responsive: true,
					maintainAspectRatio: false,
				},
			};
		},
		methods: {
			gotoSMS(comp) {
				bus.$emit("switchToSMS", comp);
			},
			ldy(comp) {
				bus.$emit("ldy", comp);
			},
			ldm(comp) {
				bus.$emit("ldm", comp);
			},
			ldd(comp) {
				bus.$emit("ldd", comp);
			},
			ldh(comp) {
				bus.$emit("ldh", comp);
			},
		},
		mounted() {
			fetch("/api/v1/LocSMSbyMonth")
				.then((response) => response.json())
				.then((datas) => {
					for (let i = 0; i < 20; i++) {
						this.chartData.datasets[0].data.push(datas[i].locSMSbyMonth);
					}
				});
		},
	};
</script>
