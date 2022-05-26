<template>
	<v-app>
		<v-container>
			<component v-bind:is="component" />
		</v-container>
	</v-app>
</template>

<script>
	import { Line as LineChartGenerator } from "vue-chartjs/legacy";
	import { bus } from "C:/Users/Yuvaraj/dashboardnew/src/main.js";
	import IncVoiceByDayVue from "./IncVoiceByDay.vue";
	import IncVoiceByMonthVue from "./IncVoiceByMonth.vue";
	import IncVoiceByHourVue from "./IncVoiceByHour.vue";
	import IncVoiceByYearVue from "./IncVoiceByYear.vue";
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
			IncVoiceByDayVue,
			IncVoiceByHourVue,
			IncVoiceByMonthVue,
			IncVoiceByYearVue,
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
				component: IncVoiceByDayVue,
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
							label: "Calls",
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
			gotovoice(comp) {
				bus.$emit("switchToVoice", comp);
			},
		},
		created() {
			bus.$on("invy", () => {
				this.component = IncVoiceByYearVue;
			});
			bus.$on("invd", () => {
				this.component = IncVoiceByDayVue;
			});
			bus.$on("invh", () => {
				this.component = IncVoiceByHourVue;
			});
			bus.$on("invm", () => {
				this.component = IncVoiceByMonthVue;
			});
		},
	};
</script>
