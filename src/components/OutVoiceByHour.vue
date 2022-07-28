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
					Outgoing Voice By Hour
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
					<v-btn @click="ouvy('page')"> By Year </v-btn>
					<v-spacer></v-spacer>
					<v-btn @click="ouvm('page')"> By Month </v-btn>
					<v-spacer></v-spacer>
					<v-btn @click="ouvd('page')"> By Day </v-btn>
					<v-spacer></v-spacer>
					<v-btn @click="ouvh('page')"> By Hour </v-btn>
					<v-spacer></v-spacer>
					<v-btn @click="gotovoice('page')"> Back To Voice </v-btn>
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
	import { bus } from "../main.js";

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
				default: () => {
					/* TODO document why this method 'default' is empty */
				},
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
						"0000",
						"0100",
						"0200",
						"0300",
						"0400",
						"0500",
						"0600",
						"0700",
						"0800",
						"0900",
						"1000",
						"1100",
						"1200",
						"1300",
						"1400",
						"1500",
						"1600",
						"1700",
						"1800",
						"1900",
						"2000",
						"2100",
						"2200",
						"2300",
					],
					datasets: [
						{
							label: "Calls",
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
			gotovoice(comp) {
				bus.$emit("switchToVoice", comp);
			},
			ouvh(comp) {
				bus.$emit("ouvh", comp);
			},
			ouvd(comp) {
				bus.$emit("ouvd", comp);
			},
			ouvm(comp) {
				bus.$emit("ouvm", comp);
			},
			ouvy(comp) {
				bus.$emit("ouvy", comp);
			},
		},
		mounted() {
			fetch("/api/v1/usage_vout_hourly")
				.then((response) => response.json())
				.then((datas) => {
					for (let i = 0; i < 24; i++) {
						this.chartData.datasets[0].data.push(datas[i].value / 60);
					}
				});
			//.then(console.log(this.hi))
		},
	};
</script>
