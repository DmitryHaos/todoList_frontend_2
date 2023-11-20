<template>
	<v-app-bar class="todo_header" :elevation="2">
		<h3>TodoList</h3>
		<v-btn @click="showModal = true;">
			Добавить
		</v-btn>
	</v-app-bar>
	<v-main class="todo_main">
		<v-list class="todo_list" lines="two">
			<v-list-item class="todo_list_item" v-for="(item, index) in items" :key="index" @click.stop="editStatusDone(item)">
				<template v-slot:prepend>
					<div class="text" :class="{done: item.done, important: item.important}">
						<span>{{item.text}}</span>
					</div>
				</template>
				<template v-slot:append>
					<v-btn class="button" @click="deleteItem(item.id)">
						X
					</v-btn>
				</template>
			</v-list-item>
		</v-list>
	</v-main>
	<v-dialog v-model="showModal" persistent width="1024">
		<v-card>
			<v-toolbar dark color="primary">
				<v-toolbar-title>
					<span class="text-h6">Добавление новой задачи</span>
				</v-toolbar-title>
				<v-btn icon dark @click="showModal = false">
					<v-icon>mdi-close</v-icon>
				</v-btn>
			</v-toolbar>
			<v-card-text>
				<v-container>
					<v-row>
						<v-col cols="12">
							<v-text-field label="Задача" v-model="newItem.text" required/>
						</v-col>
						<v-col cols="12">
							<v-checkbox label="Высокий приоритет" color="red" v-model="newItem.important"/>
						</v-col>
					</v-row>
				</v-container>
			</v-card-text>
			<v-card-actions>
				<v-spacer></v-spacer>
				<v-btn color="blue-darken-1" variant="text" @click="addItem" :disabled="newItem.text.length === 0">
					Добавить
				</v-btn>
			</v-card-actions>
		</v-card>
	</v-dialog>
</template>

<script>
	export default {
		name: 'TodoList',
		data() {
			return {
				currentID: 0,
				items: [
					{id: 1, done: false, important: false, text: "123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890"},
					{id: 2, done: true, important: true, text: "test-2"},
					{id: 3, done: true, important: false, text: "test-3"},
					{id: 4, done: false, important: true, text: "test-4"},
					{id: 5, done: false, important: false, text: "test-5"},
					{id: 6, done: false, important: false, text: "test-6"},
					{id: 7, done: false, important: false, text: "test-7"},
					{id: 8, done: false, important: false, text: "test-8"},
					{id: 9, done: true, important: false, text: "test-9"},
					{id: 10, done: false, important: false, text: "0"},
					{id: 11, done: false, important: false, text: "test-10"},
					{id: 12, done: false, important: false, text: "9876543210987654321098765432109876543210987654321098765432109876543210"},
					{id: 13, done: false, important: false, text: "test-12"},
					{id: 14, done: false, important: true, text: "END TEST"},
				],
				newItem: {
					text: "",
					important: false
				},
				showModal: false
			}
		},
		methods: {
			addItem(){
				this.items.push({
					id: this.currentID,
					text: this.newItem.text,
					important: this.newItem.important,
					done: false
				});
				this.newItem = {
					text: "",
					important: false
				};
				this.currentID++;
				this.showModal = false;
			},
			deleteItem(item_id){
				this.items = this.items.filter(item => item.id !== item_id)
			},
			editStatusDone(item){
				item.done ^= true;
			}
		},
		mounted(){
			this.currentID = this.items.length + 1;
		}
	}
</script>

<style name="app-bar">
	.todo_header > .v-toolbar__content{
		justify-content: space-between;
		align-items: center;
		background-color: #8000FF;
		padding: 2px;
	}
	.todo_header > .v-toolbar__content > h3{
		color: white;
		font-weight: bold;
		user-select: none;
		margin: 4px 4px 4px 8px;
	}
	.todo_header > .v-toolbar__content > .v-btn{
		background-color: white;
		margin: 4px;
		padding: 2px;
		font-weight: bold;
		border-radius: 5px;
	}
</style>

<style name="main" scoped>
	.todo_main > .todo_list{
		margin: 0;
		padding: 0;
		height: 100%;
		background-color: #A497D9;
	}
	.todo_main > .todo_list > .todo_list_item{
		display: flex;
		justify-content: space-between;
		margin: 5px;
		border: 1px solid black;
		color: #000000;
		background-color: white;
		user-select: none;
	}
	.todo_main > .todo_list > .todo_list_item  .text{
		margin: 0px 5px;
		overflow-wrap: anywhere;
	}
	.todo_main > .todo_list > .todo_list_item .button{
		margin: 0px 0px 0px 5px;
		color: #FF0000;
	}
</style>

<style name="custom" scoped>
	.done{
		text-decoration: line-through;
		color: #888888 !important;
	}
	.important{
		color: #FF0000;
	}
</style>