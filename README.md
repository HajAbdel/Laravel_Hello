# Laravel commands :
popular Laravel commands

## 1. Create Project

cmd :
```bash 
composer create-project laravel/laravel hello_laravel
```

or use this one for assistance :

cmd :
```bash 
laravel new hello_laravel
```

## 2. Change Dir to Project

cmd :
```bash
cd hello_laravel
```

## 3. Run Server (default port 8000)

cmd :
```bash
php artisan serve --port=8008
```

## 4. Generate Model

cmd :
```bash
php artisan make:model Product
```

## 5. Generate controller (in app/Http/Controllers/)

- vide (sans méthodes par défaut)

cmd :
```bash
php artisan make:controller ProductController
```

generated code :
```php
<?php
namespace App\Http\Controllers;
use Illuminate\Http\Request;
class Nom_Controller extends Controller
{
    //
}
```

- to generate controller + full CRUD methodes + full CRUD routes

cmd :
```bash
php artisan make:controller ProductController --resource
```

generated code :

```php
<?php
namespace App\Http\Controllers;
use Illuminate\Http\Request;
class NomController extends Controller
{
    public function index()      {} // Liste des ressources
    public function create()     {} // Formulaire de création
    public function store(Request $request)  {} // Enregistrer la ressource
    public function show($id)    {} // Afficher une ressource
    public function edit($id)    {} // Formulaire de modification
    public function update(Request $request, $id) {} // Mettre à jour
    public function destroy($id) {} // Supprimer
}
```

## 6. Create migration file (in database/migrations/)

cmd :
```bash
php artisan make:migration create_products_table
```

## 7. Generate factory file of model (to generate fake data)

cmd :
```bash
php artisan make:factory ProductFactory --model=Product
```

## 8. Generate seeder class (in database/seeders/ folder)

cmd :
```bash
php artisan make:seeder ProductSeeder
```

## 4.5.6.7.8. Generate all in one cmd : model + controller (with resources) + migration + factory + seeds

use : --all or -crmfs

cmd :
```bash
php artisan make:model Product -crmfs
```

## 9. Add routes: (in routes/web.php)

- get

code :
```php
Route::get('/products', [ProductController::class, 'index']);
```

- Route Groups + middleware

code :
```php
Route::prefix('admin')->middleware('auth')->group(function () {
    Route::resource('posts', AdminPostController::class);
});
```

- Route Naming

code :
```php
Route::get('/dashboard', [DashboardController::class, 'index'])->name('dashboard');
```
Then use it in views:

html code :
```html
<a href="{{ route('dashboard') }}">Dashboard</a>
```

## 10. Generate middleware (in app/Http/Middleware)

cmd :
```bash
php artisan make:middleware CheckSomething
```

generated code :
```php
<?php
namespace App\Http\Middleware;
use Closure;
use Illuminate\Http\Request;
use Symfony\Component\HttpFoundation\Response;
class CheckSomething
{
    public function handle(Request $request, Closure $next): Response
    {
        // Example logic
        if ($request->user() && $request->user()->is_admin) {
            return $next($request);
        }

        return redirect('/home');
    }
}

**Register the middleware**
- Route-specific: Apply only when used in routes → register in $routeMiddleware.
- Global: Apply to every request → add to $middleware in app/Http/Kernel.php.
code :
```php
protected $routeMiddleware = [
    // ...
    'check.something' => \App\Http\Middleware\CheckSomething::class,
];
```

**Using middleware in routes**
-  Single route:
Route::get('/admin', function () {
    // Only accessible if condition passes
})->middleware('check.something');

- Group of routes:
```php
Route::middleware(['check.something'])->group(function () {
    Route::get('/admin/dashboard', ...);
    Route::get('/admin/settings', ...);
});
```

- Using middleware in controllers
```php
public function __construct()
{
    $this->middleware('check.something');
}
```

## 11. Executes all pending migration files (Updates DB schema)

cmd :
```bash 
php artisan migrate
```

- undo the last migration

cmd :
```bash
php artisan migrate:rollback
```

- Drop all tables, then re-runs all migrations from scratch

cmd :
```bash
php artisan migrate:fresh
```

- drop all tables and re-runs migrations + run the DB seeders

cmd :
```bash
php artisan migrate:fresh --seed
```

## 12. run the seeder :

- Directly:

cmd :
```bash
php artisan db:seed --class=ProductSeeder
```

- Automatically :

cmd :
```bash
php artisan migrate:fresh --seed
```
or

cmd :
```bash
php artisan db:seed
```
but you must add seeder class to database/seeders/DatabaseSeeder.php

code:
```php
public function run()
{
  $this->call([
    TaskSeeder::class,
  ]);
}
```
