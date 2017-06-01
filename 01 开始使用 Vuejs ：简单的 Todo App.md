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


```
