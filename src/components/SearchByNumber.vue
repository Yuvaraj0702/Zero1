<template>
	<v-container>
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
				Search By Number
			</div>
			<v-card color="grey lighten-4" flat height="50px" tile>
				<v-toolbar>
					<v-app-bar-nav-icon></v-app-bar-nav-icon>

					<v-text-field hide-details single-line></v-text-field>

					<v-btn icon>
						<v-icon>mdi-magnify</v-icon>
					</v-btn>

					<v-btn icon>
						<v-icon>mdi-heart</v-icon>
					</v-btn>

					<v-btn icon>
						<v-icon>mdi-dots-vertical</v-icon>
					</v-btn>
				</v-toolbar>
			</v-card>
		</div>
	</v-container>
</template>
