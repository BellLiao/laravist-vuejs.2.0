#使用 Vue 脚手架工具进行组件化开发

> https://github.com/vuejs/vue-cli
>https://github.com/webpack/webpack

npm install -g vue-cli --registry https://registry.npm.taobao.org
npm install --global webpack --registry https://registry.npm.taobao.org

vue init webpack vuejs-2.0-cli
![](image/screenshot_1496381549058.png)

cd vuejs-2.0-cli/
npm install --registry https://registry.npm.taobao.org
npm run dev

把之前的组件融合到这个项目中

index.html
```
<link rel="stylesheet" href="https://cdn.bootcss.com/bootstrap/3.3.7/css/bootstrap.min.css">

<body>
<nav class="navbar navbar-default navbar-static-top">
    <div class="container-fluid">
        <!-- Brand and toggle get grouped for better mobile display -->
        <div class="navbar-header">
            <a class="navbar-brand" href="#">Vue js 2.0</a>
        </div>
    </div><!-- /.container-fluid -->
</nav>
<div id="app"></div>
<!-- built files will be auto injected -->
</body>
```

src/App.vue
```
<template>
    <div class="container" id="app">
        <div class="row">
            <div class="col-md-8 col-md-offset-2">
                <div class="panel panel-default">
                    <div class="panel-heading">Welcome Vue js 2.0 Tutorial</div>
                    <div class="panel-body">
                        <img src="./assets/logo.png">
                        <hello></hello>
                        <h1>{{ message }} {{ todoCount }}</h1>
                        <todos :todos="todos"></todos>
                        <todo-form :todos="todos"></todo-form>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import Hello from './components/Hello'
    import Todos from './components/Todos'
    import TodoForm from './components/TodoForm'

    export default {
        name: 'app',
        data(){
            return {
                message: 'My Todos',
                todos: [
                    {id: 1, title: 'Learn Vuejs', completed: false}
                ]
            }
        },
        computed: {
            todoCount(){
                return this.todos.length;
            }
        },
        components: {
            Hello, Todos, TodoForm
        }
    }
</script>
```

src/components/Todos.vue
```
<template>
    <ul class="list-group">
        <li class="list-group-item" v-bind:class="{ 'completed':todo.completed }" v-for="(todo, index) in todos">
            {{ todo.title }}
            <button class="btn btn-warning btn-xs pull-right" v-on:click="deleteTodo(index)">Delete</button>
            <button class="btn btn-xs pull-right" v-bind:class="[todo.completed ? 'btn-danger' : 'btn-success']"
                    v-on:click="toggleCompletion(todo)">{{ todo.completed ? 'undo' : 'completed' }}
            </button>
        </li>
    </ul>
</template>

<script>
    export default {
        props: ['todos'],
        methods: {
            deleteTodo(index){
                this.todos.splice(index, 1);
            },
            toggleCompletion(todo){
                todo.completed = !todo.completed;
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .completed {
        color: green;
        text-decoration: line-through;
    }
</style>	
```

TodoForm.vue
```
<template>
    <form v-on:submit.prevent="addTodo(newTodo)">
        <div class="form-group">
            <input type="text" class="form-control" placeholder="Add a new todo"
                   v-model="newTodo.title">
        </div>
        <div class="form-group">
            <button class="btn btn-success" type="submit">Add Todo</button>
        </div>
    </form>
</template>

<script>
    export default {
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
    }
</script>
```