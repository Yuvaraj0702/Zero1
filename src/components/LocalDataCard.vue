<template>
	<v-app>
		<v-conatiner>
			<component v-bind:is="component" />
		</v-conatiner>
	</v-app>
</template>

<script>
	import { Line as LineChartGenerator } from "vue-chartjs/legacy";
	import { bus } from "../main.js";
	import LocDataByDay from "./LocDataByDay.vue";
	import LocDataByHour from "./LocDataByHour.vue";
	import LocDataByMonth from "./LocDataByMonth.vue";
	import LocDataByYear from "./LocDataByYear.vue";

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
			LocDataByDay,
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
				component: LocDataByDay,
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
			bus.$on("ldy", () => {
				this.component = LocDataByYear;
			});
			bus.$on("ldm", () => {
				this.component = LocDataByMonth;
			});
			bus.$on("ldh", () => {
				this.component = LocDataByHour;
			});
			bus.$on("ldd", () => {
				this.component = LocDataByDay;
			});
		},
	};
</script>
