#使用 Vuejs 组件化开发

```
<link rel="stylesheet" href="https://cdn.bootcss.com/bootstrap/3.3.7/css/bootstrap.min.css">
<style>
    .completed{ color: green; text-decoration: line-through; }
</style>

<nav class="navbar navbar-default navbar-static-top">
    <div class="container-fluid">
        <!-- Brand and toggle get grouped for better mobile display -->
        <div class="navbar-header">
            <a class="navbar-brand" href="#">Vue js 2.0</a>
        </div>
    </div><!-- /.container-fluid -->
</nav>

<div class="container" id="app">
    <div class="row">
        <div class="col-md-8 col-md-offset-2">
            <div class="panel panel-default">
                <div class="panel-heading">Welcome Vue js 2.0 Tutorial</div>
                <div class="panel-body">
                    <h1>{{ message }} {{ todoCount }}</h1>
                    <todo-items :todos="todos"></todo-items>
                    <todo-form :todos="todos"></todo-form>
                </div>
            </div>
        </div>
    </div>
</div>
<script type="text/x-template" id="todo-item-template">
    <ul class="list-group">
        <li class="list-group-item" v-bind:class="{ 'completed':todo.completed }" v-for="(todo, index) in todos">
            {{ todo.title }}
            <button class="btn btn-warning btn-xs pull-right" v-on:click="deleteTodo(index)">Delete</button>
            <button class="btn btn-xs pull-right" v-bind:class="[todo.completed ? 'btn-danger' : 'btn-success']" v-on:click="toggleCompletion(todo)">{{ todo.completed ? 'undo' : 'completed' }}</button>
        </li>
    </ul>
</script>
<script type="text/x-template" id="todo-add-form-template">
    <form v-on:submit.prevent="addTodo(newTodo)">
        <div class="form-group">
            <input type="text" class="form-control" placeholder="Add a new todo"
                   v-model="newTodo.title">
        </div>
        <div class="form-group">
            <button class="btn btn-success" type="submit">Add Todo</button>
        </div>
    </form>
</script>
<script src="js/vue.js"></script>
<script>
    Vue.component('todo-items', {
        template: '#todo-item-template',
        props: ['todos'],
        methods: {
            deleteTodo(index){
                this.todos.splice(index, 1);
            },
            toggleCompletion(todo){
                todo.completed = !todo.completed;
            }
        }
    });

    Vue.component('todo-form', {
        template: '#todo-add-form-template',
        props: ['todos'],
        data(){
            return {
                newTodo: {id: null, title: '', completed: false}
            }
        },
        methods: {
            addTodo(newTodo){
                this.todos.push(newTodo);
                this.newTodo = {id: null, title: '', completed: false};
            }
        }
    });

    new Vue({
        el: '#app',
        data: {
            message: 'My Todos',
            todos: [
                {id: 1, title: 'Learn Vuejs', completed: false}
            ]
        },
        computed: {
            todoCount(){
                return this.todos.length;
            }
        }
    });
</script>
```