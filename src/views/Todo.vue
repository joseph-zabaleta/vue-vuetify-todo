<template>
	<div class="home">
		<v-text-field
			v-model="newTaskTitle"
			@click:append="addTask"
			@keyup.enter="addTask"
			class="pa-3"
			outlined
			hide-details
			clearable
			label="Add New Task"
			append-icon="mdi-plus"
		></v-text-field>
		<v-list flat class="pt-0">
			<div v-for="task in tasks" :key="task.id">
				<v-list-item
					@click="completeTask(task.id)"
					:class="{ 'green lighten-3': task.done }"
				>
					<template v-slot:default>
						<v-list-item-action>
							<v-checkbox
								:input-value="task.done"
								color="primary"
							></v-checkbox>
						</v-list-item-action>

						<v-list-item-content>
							<v-list-item-title
								:class="{
									'text-decoration-line-through': task.done,
								}"
								>{{ task.title }}</v-list-item-title
							>
						</v-list-item-content>
						<v-list-item-action>
							<v-btn icon @click.stop="deleteTask(task.id)">
								<v-icon color="grey lighten-1"
									>mdi-trash-can</v-icon
								>
							</v-btn>
						</v-list-item-action>
					</template>
				</v-list-item>
				<v-divider></v-divider>
			</div>
		</v-list>
	</div>
</template>

<script>
export default {
	name: 'Home',
	data() {
		return {
			newTaskTitle: '',
			tasks: [
				{
					id: 1,
					title: 'Learn Vue',
					done: true,
				},
				{
					id: 2,
					title: 'Learn Vuetify',
					done: false,
				},
				{
					id: 3,
					title: 'Learn Kubernetes',
					done: false,
				},
			],
		};
	},
	methods: {
		addTask() {
			let newTask = {
				id: Date.now(),
				title: this.newTaskTitle,
				done: false,
			};

			this.tasks.push(newTask);
			this.newTaskTitle = '';
		},
		completeTask(id) {
			let task = this.tasks.filter((task) => task.id === id)[0];
			task.done = !task.done;
		},
		deleteTask(id) {
			this.tasks = this.tasks.filter((task) => task.id !== id);
		},
	},
};
</script>
