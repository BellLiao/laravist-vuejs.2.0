#Vuejs 2.0 使用 vue-router 处理前端路由

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

