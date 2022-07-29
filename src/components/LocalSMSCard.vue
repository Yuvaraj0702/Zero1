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
	import LocSMSByDayVue from "./LocSMSByDay.vue";
	import LocSMSByHourVue from "./LocSMSByHour.vue";
	import LocSMSByMonthVue from "./LocSMSByMonth.vue";
	import LocSMSByYearVue from "./LocSMSByYear.vue";
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
			LocSMSByDayVue,
			LocSMSByHourVue,
			LocSMSByMonthVue,
			LocSMSByYearVue,
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
				component: LocSMSByDayVue,
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
							label: "SMS",
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
			gotosms(comp) {
				bus.$emit("switchToSMS", comp);
			},
		},
		created() {
			bus.$on("ldy", () => {
				this.component = LocSMSByYearVue;
			});
			bus.$on("ldd", () => {
				this.component = LocSMSByDayVue;
			});
			bus.$on("ldh", () => {
				this.component = LocSMSByHourVue;
			});
			bus.$on("ldm", () => {
				this.component = LocSMSByMonthVue;
			});
		},
	};
</script>
