<!-- @format -->

# Section Title: Routers

### Typical methods of Laravel’s resource controllers

| Verb | URL | method | Name | Description |
| ---- | --- | ------ | ---- | ----------- |

GET | tasks | index() | tasks.index | Show all tasks
GET | tasks/create | create() | tasks.create | Show the create task form
POST | tasks | store() | tasks.store | Accept form submission from the create task form
GET | tasks/{task} | show() | tasks.show | Show one task
GET | tasks/{task}/edit | edit() | tasks.edit | Edit one task
PUT | tasks/{task}| update() | tasks.update | Accept form submission from the edit task form
DELETE | tasks/{task} | destroy() | tasks.destroy | Delete one task

- where `{task}` is a reference to a model called Tas
- by default the id field is used for model binding
- do `{task:slug}` to use another field for the binding e.g slug

### Route Definitions

- define your web routes in `routes/web.php`
- and API routes in `routes/api.php`

#### Routing with closures

- the simplest way to define a route is to match a path (e.g., /) with a closure

```php
// routes/web.php
Route::get('/', function () {
 return 'Hello, World!';
});
```

- Note that we **return** our content and **don’t** `echo` or `print` it. ( this is to allow it to continue flowing through the response stack and the middleware before it is displayed to the user)

##### Route Verbs

- apart from `get()`, `post()`, `put()`, `delete()`, we also have `any()`, `match()`

```php
Route::any('/', function () {
 // Handle any verb request to this route
});
Route::match(['get', 'post'], '/', function () {
 // Handle GET or POST requests to this route
});

```

#### Routing with controller methods

```php
Route::get('/', [WelcomeController::class, 'index']);
```
