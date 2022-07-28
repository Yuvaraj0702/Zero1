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
	import OutVoiceByDayVue from "./OutVoiceByDay.vue";
	import OutVoiceByHourVue from "./OutVoiceByHour.vue";
	import OutVoiceByMonthVue from "./OutVoiceByMonth.vue";
	import OutVoiceByYearVue from "./OutVoiceByYear.vue";
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
			OutVoiceByDayVue,
			OutVoiceByHourVue,
			OutVoiceByMonthVue,
			OutVoiceByYearVue,
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
				component: OutVoiceByDayVue,
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
			bus.$on("ouvy", () => {
				this.component = OutVoiceByYearVue;
			});
			bus.$on("ouvd", () => {
				this.component = OutVoiceByDayVue;
			});
			bus.$on("ouvh", () => {
				this.component = OutVoiceByHourVue;
			});
			bus.$on("ouvm", () => {
				this.component = OutVoiceByMonthVue;
			});
		},
	};
</script>
