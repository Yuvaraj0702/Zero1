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
					International Data By Year
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
					<v-btn @click="idy('page')"> By Year </v-btn>
					<v-spacer></v-spacer>
					<v-btn @click="idm('page')"> By Month </v-btn>
					<v-spacer></v-spacer>
					<v-btn @click="idd('page')"> By Day </v-btn>
					<v-spacer></v-spacer>
					<v-btn @click="idh('page')"> By Hour </v-btn>
					<v-spacer></v-spacer>
					<v-btn @click="gotodata('page')"> Back To Data </v-btn>
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
						"2017",
						"2018",
						"2019",
						"2020",
						"2021",
						"2022",
					],
					datasets: [
						{
							label: "Data",
							backgroundColor: "red",
							data: [40, 39, 10, 40, 39, 80, 40],
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
			gotodata(comp) {
				bus.$emit("switchToData", comp);
			},
			idy(comp) {
				bus.$emit("idy", comp);
			},
			idm(comp) {
				bus.$emit("idm", comp);
			},
			idh(comp) {
				bus.$emit("idh", comp);
			},
			idd(comp) {
				bus.$emit("idd", comp);
			},
		},
	};
</script>
