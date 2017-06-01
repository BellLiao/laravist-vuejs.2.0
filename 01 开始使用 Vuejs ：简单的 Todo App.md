#开始使用 Vuejs ：简单的 Todo App

```
<link rel="stylesheet" href="https://cdn.bootcss.com/bootstrap/3.3.7/css/bootstrap.min.css">

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
                    <h1>{{ message }}</h1>
                    <input type="text" class="form-control" v-model="message">
                </div>
            </div>
        </div>
    </div>
</div>

<script src="js/vue.js"></script>
<script>
    new Vue({
        el: '#app',
        data: {
            message: 'Hello World'
        }
    });
</script>
```

```
<link rel="stylesheet" href="https://cdn.bootcss.com/bootstrap/3.3.7/css/bootstrap.min.css">

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
                    <h1>{{ message }}</h1>
                    <ul class="list-group">
                        <li class="list-group-item" v-for="(todo, index) in todos">
                            {{ todo.title }}
                            <button class="btn btn-warning btn-xs pull-right" v-on:click="deleteTodo(index)">Delete</button>
                        </li>
                    </ul>
                    <form v-on:submit.prevent="addTodo(newTodo)">
                        <div class="form-group">
                            <input type="text" class="form-control" placeholder="Add a new todo"
                                   v-model="newTodo.title">
                        </div>
                        <div class="form-group">
                            <button class="btn btn-success" type="submit">Add Todo</button>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </div>
</div>

<script src="js/vue.js"></script>
<script>
    new Vue({
        el: '#app',
        data: {
            message: 'My Todos',
            todos: [
                {id: 1, title: 'Learn Vuejs'}
            ],
            newTodo: {id: null, title: ''}
        },
        methods: {
            addTodo(newTodo){
                this.todos.push(newTodo);
                this.newTodo = {id: null, title: ''};
            },
            deleteTodo(index){
                this.todos.splice(index, 1);
            }
        }
    });
</script>
```
