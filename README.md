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
After that, open company migration  file inside laravel-9-crud/database/migrations/ directory. And then update the function up() with the following code:

public function up()
{
    Schema::create('companies', function (Blueprint $table) {
        $table->id();
        $table->string('name');
        $table->string('email');
        $table->string('address');
        $table->timestamps();
    });
}
app/Models/Company.php

<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Company extends Model
{
    use HasFactory;

    protected $fillable = ['name', 'email', 'address'];
}
Then, open again command prompt and run the following command to create tables in the database:

php artisan migrate


Step 4 – Create Company Controller By Artisan Command
Create a controller by using the following command on the command prompt to create a controller file:

php artisan make:controller CompanyController
After that, visit app/Http/controllers and open the CompanyController.php file. And update the following code into it:

<?php

namespace App\Http\Controllers;
use App\Models\Company;
use Illuminate\Http\Request;

class CompanyController extends Controller
{
    /**
    * Display a listing of the resource.
    *
    * @return \Illuminate\Http\Response
    */
    public function index()
    {
        $companies = Company::orderBy('id','desc')->paginate(5);
        return view('companies.index', compact('companies'));
    }

    /**
    * Show the form for creating a new resource.
    *
    * @return \Illuminate\Http\Response
    */
    public function create()
    {
        return view('companies.create');
    }

    /**
    * Store a newly created resource in storage.
    *
    * @param  \Illuminate\Http\Request  $request
    * @return \Illuminate\Http\Response
    */
    public function store(Request $request)
    {
        $request->validate([
            'name' => 'required',
            'email' => 'required',
            'address' => 'required',
        ]);
        
        Company::create($request->post());

        return redirect()->route('companies.index')->with('success','Company has been created successfully.');
    }

    /**
    * Display the specified resource.
    *
    * @param  \App\company  $company
    * @return \Illuminate\Http\Response
    */
    public function show(Company $company)
    {
        return view('companies.show',compact('company'));
    }

    /**
    * Show the form for editing the specified resource.
    *
    * @param  \App\Company  $company
    * @return \Illuminate\Http\Response
    */
    public function edit(Company $company)
    {
        return view('companies.edit',compact('company'));
    }

    /**
    * Update the specified resource in storage.
    *
    * @param  \Illuminate\Http\Request  $request
    * @param  \App\company  $company
    * @return \Illuminate\Http\Response
    */
    public function update(Request $request, Company $company)
    {
        $request->validate([
            'name' => 'required',
            'email' => 'required',
            'address' => 'required',
        ]);
        
        $company->fill($request->post())->save();

        return redirect()->route('companies.index')->with('success','Company Has Been updated successfully');
    }

    /**
    * Remove the specified resource from storage.
    *
    * @param  \App\Company  $company
    * @return \Illuminate\Http\Response
    */
    public function destroy(Company $company)
    {
        $company->delete();
        return redirect()->route('companies.index')->with('success','Company has been deleted successfully');
    }
}
Step 5 – Create Routes
Then create routes for laravel crud app. So, open the web.php file from the routes directory of laravel CRUD app. And update the following routes into the web.php file:

use App\Http\Controllers\CompanyController;
 
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

![image](https://user-images.githubusercontent.com/42266013/219767356-b53724f5-1c22-4d3e-9a13-fab42483c6f5.png)


![image](https://user-images.githubusercontent.com/42266013/219767594-eb9db8b9-5dfe-4181-87c3-503e4ff15ad0.png)

