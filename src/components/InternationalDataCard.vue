<template>
	<v-app>
		<v-container>
			<component v-bind:is="component" />
		</v-container>
	</v-app>
</template>

<script>
	import { Line as LineChartGenerator } from "vue-chartjs/legacy";
	import { bus } from "../main.js";
	import IntDataByDayVue from "./IntDataByDay.vue";
	import IntDataByHourVue from "./IntDataByHour.vue";
	import IntDataByMonthVue from "./IntDataByMonth.vue";
	import IntDataByYearVue from "./IntDataByYear.vue";

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
			IntDataByDayVue,
			IntDataByHourVue,
			IntDataByYearVue,
			IntDataByMonthVue,
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
				component: IntDataByDayVue,
				chartData: {
					labels: [
						"January",
						"February",
						"March",
						"April",
						"May",
						"June",
						"July",
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
		},
		created() {
			bus.$on("idy", () => {
				this.component = IntDataByYearVue;
			});
			bus.$on("idd", () => {
				this.component = IntDataByDayVue;
			});
			bus.$on("idh", () => {
				this.component = IntDataByHourVue;
			});
			bus.$on("idm", () => {
				this.component = IntDataByMonthVue;
			});
		},
	};
</script>
