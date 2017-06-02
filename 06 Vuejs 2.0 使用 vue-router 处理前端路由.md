#Vuejs 2.0 使用 vue-router 处理前端路由

>https://github.com/vuejs/vue-router

cd laravel-package/
php artisan make:model Todo -m

2017_06_02_110139_create_todos_table.php
```
public function up()
{
    Schema::create('todos', function (Blueprint $table) {
        $table->increments('id');
        $table->string('title');
        $table->tinyInteger('completed')->default(0);
        $table->timestamps();
    });
}
```

php artisan migrate

Todo.php
```
protected $fillable = ['title'];
```

php artisan tinker
namespace App
factory(Todo::class, 20)->create()

api.php
```
Route::get('/todos', function(){
    $todos = \App\Todo::all();
    return $todos;
})->middleware('cors:api');
```

![](image/screenshot_1496403289289.png)

npm install vue-router --registry https://registry.npm.taobao.org

main.js
```
import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'
import VueRouter from 'vue-router'
import App from './App'
import Todos from './components/Todos'
import Todo from './components/Todo'

Vue.config.productionTip = false

Vue.use(VueAxios, axios)
Vue.use(VueRouter)

const routes = [
  { path: '/', component: Todos },
  { path: '/todo/:id', component: Todo, name: 'todo' }
]

const router = new VueRouter({
  routes // short for routes: routes
})

/* eslint-disable no-new */
new Vue({
  el: '#app',
  template: '<App/>',
  components: { App },
  router
})
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
            <router-view :todos="todos"></router-view>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import Hello from './components/Hello'

  export default {
    name: 'app',
    data(){
      return {
        message: 'My Todos',
        todos: []
      }
    },
    mounted(){
      this.axios.get('http://laravel-package.dev/api/todos').then(response=>{
        this.todos = response.data;
        console.log(response);
      });
    },
    computed: {
      todoCount(){
        return this.todos.length;
      }
    },
    components: {
      Hello
    }
  }
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

```
