# Laravel / Livewire / AlpineJS : Hello
Laravel with Livewire &amp; AlpineJS : a "Hello World" code

## 1. Create Project
`composer create-project laravel/laravel hello_laravel`

**to use this one for assistance**

`laravel new hello_laravel`

## 2. Change Dir to Project
`cd hello_laravel`

## 3. Run Server (default port 8000)
`php artisan serve --port=8008`

## 4. Generate Model
`php artisan make:model Product`

## 5. Create migration file (database/migrations/ folder)
`php artisan make:migration create_products_table`

## 6. Create factory file + link it to its model (to generate fake data)

`php artisan make:factory ProductFactory --model=Product`

## 7. Create seeder class (in database/seeders/ folder)

`php artisan make:seeder ProductSeeder`

**run the seeder**

`php artisan db:seed --class=ProductSeeder`



php artisan migrate:fresh --seed



## 6. Executes all pending migration files (Updates DB schema)
`php artisan migrate`

**to undo the last migration**

`php artisan migrate:rollback`

**to Drops all tables, then re-runs all migrations from scratch**

`php artisan migrate:fresh`

**drops all tables and re-runs migrations + run the DB seeders

`php artisan migrate:fresh --seed`



