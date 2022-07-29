<template>
	<v-app>
		<v-app-bar
			app
			absolute
			color="#FF0000"
			dark
			prominent
			scroll-target="#scrolling-techniques"
		>
			<v-img
				alt="Zero1 Logo"
				class="shrink mr-2"
				contain
				src="https://zero1.sg/img/logo.png"
				transition="scale-transition"
				width="120"
				height="75"
			/>
			<v-spacer></v-spacer>
			<v-card height="120" class="d-flex align-center" color="#FF0000" flat>
				<h1>Zero1 Employee Portal</h1>
			</v-card>

			<v-spacer></v-spacer>

			<v-btn
				large
				text
				onclick="window.location.href = 'http://localhost:3001/';"
			>
				<!-- Localhost 3000 or your port hosting the login page -->
				<!-- this is to -->
				Back to portal
				<v-icon color="white" small right>mdi-logout-variant</v-icon>
			</v-btn>

			<template v-slot:extension>
				<v-tabs fixed-tabs align-with-title>
					<v-tab @click="gotovoice">Voice</v-tab>
					<v-tab @click="gotodata">Data</v-tab>
					<v-tab @click="gotoIDD">IDD</v-tab>
					<v-tab @click="gotoSMS">SMS</v-tab>
					<v-tab @click="gotoroaming">Roaming</v-tab>
					<v-tab @click="gotosearch">Search By Number</v-tab>
				</v-tabs>
			</template>
		</v-app-bar>

		<v-main>
			<component v-bind:is="component" />
		</v-main>
	</v-app>
</template>

<script>
	import { bus } from "C:/Users/Yuvaraj/dashboardnew/src/main.js";
	import VoicePage from "./VoicePage.vue";
	import RoamingPage from "./RoamingPage.vue";
	import SMS from "./SMS.vue";
	import SearchByNumber from "./SearchByNumber.vue";
	import DataPage from "./DataPage.vue";
	import IDD from "./IDD.vue";
	import InVoiceCard from "./InVoiceCard.vue";
	import OutVoiceCard from "./OutVoiceCard.vue";
	import LocalDataCard from "./LocalDataCard.vue";
	import InternationalDataCard from "./InternationalDataCard.vue";
	import InternationalSMSCard from "./InternationalSMSCard.vue";
	import InternationalRoamingCard from "./InternationalRoamingCard.vue";
	import LocalSMSCard from "./LocalSMSCard.vue";
	import LocalRoamingCard from "./LocalRoamingCard.vue";
	import HomeRoamingCard from "./HomeRoamingCard.vue";

	export default {
		name: "App",

		components: {},

		data: () => ({
			component: VoicePage,
		}),
		created() {
			bus.$on("switchToOutGraph", () => {
				this.component = OutVoiceCard;
			});
			bus.$on("switchToIncGraph", () => {
				this.component = InVoiceCard;
			});
			bus.$on("switchToIDD", () => {
				this.component = IDD;
			});
			bus.$on("switchToLocalD", () => {
				this.component = LocalDataCard;
			});
			bus.$on("switchToIntD", () => {
				this.component = InternationalDataCard;
			});
			bus.$on("switchToLocalSMSCard", () => {
				this.component = LocalSMSCard;
			});
			bus.$on("switchToIntSMSCard", () => {
				this.component = InternationalSMSCard;
			});
			bus.$on("switchTolr", () => {
				this.component = LocalRoamingCard;
			});
			bus.$on("switchToir", () => {
				this.component = InternationalRoamingCard;
			});
			bus.$on("switchTohr", () => {
				this.component = HomeRoamingCard;
			});
			bus.$on("switchToVoice", () => {
				this.component = VoicePage;
			});
			bus.$on("switchToRoam", () => {
				this.component = RoamingPage;
			});
			bus.$on("switchToSMS", () => {
				this.component = SMS;
			});
			bus.$on("switchToData", () => {
				this.component = DataPage;
			});
		},
		methods: {
			gotovoice() {
				if (this.component !== VoicePage) {
					this.component = VoicePage;
				}
			},
			gotodata() {
				if (this.component !== DataPage) {
					this.component = DataPage;
				}
			},
			gotoIDD() {
				if (this.component !== IDD) {
					this.component = IDD;
				}
			},
			gotoSMS() {
				if (this.component !== SMS) {
					this.component = SMS;
				}
			},
			gotoroaming() {
				if (this.component !== RoamingPage) {
					this.component = RoamingPage;
				}
			},
			gotosearch() {
				if (this.component !== SearchByNumber) {
					this.component = SearchByNumber;
				}
			},
			logOut(comp) {
				bus.$emit("switchToLogin", comp);
			},
		},
	};
</script>
