
 

# Laravel9CRUD

Please follow the below comments to DO CRUD Operation in Laravel


Step 1 – Download Laravel 9 App
First of all, download or install laravel 9 new setup. So, open the terminal and type the following command to install the new laravel 9 app into your machine:

composer create-project --prefer-dist laravel/laravel:^9.0 laravel-9-crud
Step 2 – Setup Database with App
Setup database with your downloaded/installed laravel app. So, you need to find the .env file and setup database details as follows:

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=database-name
DB_USERNAME=database-user-name
DB_PASSWORD=database-password

Step 3 – Create Company Model & Migration For CRUD App
Open again your command prompt. And run the following command on it. To create model and migration file for form:

php artisan make:model Company -m
 
app/Models/Company.php

 
Then, open again command prompt and run the following command to create tables in the database:

php artisan migrate


Step 4 – Create Company Controller By Artisan Command
Create a controller by using the following command on the command prompt to create a controller file:

php artisan make:controller CompanyController
After that, visit app/Http/controllers and open the CompanyController.php file. And update the following code into it:

 
Step 5 – Create Routes
Then create routes for laravel crud app. So, open the web.php file from the routes directory of laravel CRUD app. And update the following routes into the web.php file:

 
 
Route::resource('companies', CompanyController::class);

Step 6 – Create Blade Views File
Create the directory and some blade view, see the following:

Make Directory Name Companies
index.blade.php
create.blade.php
edit.blade.php
Create directory name companies inside the resources/views directory.


Step 7 – Run Development Server
In the last step, open a command prompt and run the following command to start the development server:

php artisan serve
Then open your browser and hit the following URL on it:

http://127.0.0.1:8000

 

![image](https://user-images.githubusercontent.com/42266013/219768083-de7a3296-f18c-42a6-b00b-f0ce315e8f03.png)




