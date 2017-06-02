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

index.html
```
<link rel="stylesheet" href="https://cdn.bootcss.com/bootstrap/3.3.7/css/bootstrap.min.css">
```

App.vue
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