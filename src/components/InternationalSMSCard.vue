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
	import IntSMSByDayVue from "./IntSMSByDay.vue";
	import IntSMSbyHourVue from "./IntSMSbyHour.vue";
	import IntSMSByMonthVue from "./IntSMSByMonth.vue";
	import IntSMSByYearVue from "./IntSMSByYear.vue";
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
			IntSMSByDayVue,
			IntSMSByMonthVue,
			IntSMSByYearVue,
			IntSMSbyHourVue,
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
				component: IntSMSByDayVue,
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
			bus.$on("insy", () => {
				this.component = IntSMSByYearVue;
			});
			bus.$on("insd", () => {
				this.component = IntSMSByDayVue;
			});
			bus.$on("insh", () => {
				this.component = IntSMSbyHourVue;
			});
			bus.$on("insm", () => {
				this.component = IntSMSByMonthVue;
			});
		},
	};
</script>
