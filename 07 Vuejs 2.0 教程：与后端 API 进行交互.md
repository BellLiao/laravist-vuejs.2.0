#Vuejs 2.0 教程：与后端 API 进行交互

api.php
```
Route::post('/todo/create', function (Request $request) {
    $data = ['title' => $request->get('title')];
    $todo = App\Todo::create($data);
    return $todo;
})->middleware('api', 'cors');

Route::patch('/todo/{id}/completed', function ($id) {
    $todo = App\Todo::find($id);
    $todo->completed = !$todo->completed;
    $todo->save();
    return $todo;
})->middleware('api', 'cors');

Route::patch('/todo/{id}/delete', function ($id) {
    $todo = App\Todo::find($id);
    $todo->delete();
    return response()->json(['deleted']);
})->middleware('api', 'cors');
```

TodoForm.vue
```
addTodo(newTodo){
    this.axios.post('http://laravel-package.dev/api/todo/create', {title: this.newTodo.title}).then(response => {
        console.log(response.data);
        this.todos.push(response.data);
        this.newTodo = {id: null, title: '', completed: false};
    });
}
```

Todos.vue
```
deleteTodo(index){
    this.axios.patch('http://laravel-package.dev/api/todo/' + this.todos[index].id + '/delete').then(response => {
        console.log(response.data);
        this.todos.splice(index, 1);
    });
},
toggleCompletion(todo){
    this.axios.patch('http://laravel-package.dev/api/todo/' + todo.id + '/completed').then(response => {
        console.log(response.data);
        todo.completed = !todo.completed;
    });
}
```
