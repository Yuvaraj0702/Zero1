<template>
	<v-conatiner>
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
		<div id="div1">
			<v-container>
				<v-row justify="center">
					<v-card class="mx-auto my-12" width="600">
						<v-card-text class="d-flex justify-center">
							<v-img contain height="180" src="https://zero1.sg/img/logo.png">
							</v-img>
						</v-card-text>

						<v-card-text class="d-flex justify-center mb-5">
							<h1>Zero1 Employee Login</h1>
						</v-card-text>

						<v-card-actions class="d-flex justify-center">
							<v-btn
								elevation="2"
								raised
								rounded
								tile
								x-large
								color="red"
								class="justify-center white--text"
								@click="logIn('MainPage')"
								>Login</v-btn
							>
						</v-card-actions>
					</v-card>
				</v-row>
			</v-container>
		</div>
	</v-conatiner>
</template>

<script>
	import { bus } from "../main.js";

	export default {
		name: "LoginPage",
		components: {
			//
		},

		data() {
			return {
				items: ["Staff", "Customer"],
				selectedDomain: null,
				show1: false,
				show2: true,
				show3: false,
				show4: false,
				password: "Password",
				rules: {
					required: (value) => !!value || "Required.",
					min: (v) => v.length >= 8 || "Min 8 characters",
					emailMatch: () => `The email and password you entered don't match`,
				},
			};
		},

		methods: {
			change(e) {
				this.selectedDomain = e;
			},
			logIn(comp) {
				bus.$emit("switchToMain", comp);
			},
		},
	};
</script>
<style scoped>
	#div1 {
		background-color: red;
	}
</style>
