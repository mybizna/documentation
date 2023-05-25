---
description: >-
  Mybizna is an open-source ERP (Enterprise Resource Planning) solution for
  Laravel. It is developed using Laravel which is a web application framework
  with expressive, elegant syntax.
---

# How to install in Existing  Laravel Project

## Prerequisites <a href="#f144" id="f144"></a>

Before proceeding with the installation, make sure you have the following prerequisites:

1. PHP (version 8.1 or higher)
2. Composer (Dependency Manager for PHP)
3. MySQL or any other compatible database server

### Step 1 <a href="#d817" id="d817"></a>

Install the required package To install the Laravel ERP package, run the following command:

```
composer require mybizna/account
```

### Step 2 <a href="#717b" id="717b"></a>

Configure the database Open the `.env` file in the root directory of your project and modify the following lines to match your database credentials:

```
CACHE_DRIVER=database
SESSION_DRIVER=database
SESSION_DOMAIN=
SANCTUM_STATEFUL_DOMAINS=
```

### Step 3 <a href="#9853" id="9853"></a>

Edit the User model Open the `app/Models/User.php` file and add the following lines inside the `protected $fillable` array:

```
'username',
'is_admin',
'phone',
```

### Step 4 <a href="#0169" id="0169"></a>

Add class and trait to the User model Add the following lines at the top of the `app/Models/User.php` file:

```
use Spatie\Permission\Traits\HasRoles;
```

Inside the `User` model class, add the following line:

```
use HasRoles;
```

### Step 5 <a href="#6cf5" id="6cf5"></a>

Publish the following;

<pre class="language-sh" data-line-numbers><code class="lang-sh"><strong>php artisan cache:table
</strong>php artisan session:table
php artisan vendor:publish --provider="Laravel\Sanctum\SanctumServiceProvider"
php artisan vendor:publish --provider="Mybizna\Assets\Providers\MybiznaAssetsProvider"
php artisan vendor:publish --provider="Spatie\Permission\PermissionServiceProvider"
</code></pre>

* 1 is for generating the **cache** table used in managing system cache.
* 2 is for generate the **session** table used for managing system session using database.
* 3 is for publishing **santrum** migration files to be used to login to Mybizna ERP API.
* 4 is for publishing assets and database migration for adding username, phone, and email to the **users** table in the database.
* 5 is for publishing permissions configuration provided by the **Spatie/Permission** package.

&#x20;Add Sanctum's middleware to your `api` middleware group within your application's `app/Http/Kernel.php` file:

```
'api' => [
            \Laravel\Sanctum\Http\Middleware\EnsureFrontendRequestsAreStateful::class,
            'throttle:api',
            \Illuminate\Routing\Middleware\SubstituteBindings::class,
        ],
```

### Step 6 <a href="#f4e1" id="f4e1"></a>

Run database migrations To create the necessary database tables, run the following command:

```
php artisan automigrator:migrate
```

### Step 7 <a href="#7276" id="7276"></a>

Create a dummy user called _**John Doe**_ Using tinker:

```
php artisan tinker

$user = new App\Models\User();
$user->password = Hash::make('johndoe');
$user->email = 'johndoe@johndoe.com';
$user->name = 'John Doe';
$user->is_admin = 1;
$user->username = 'johndoe';
$user->phone = '0723232323';
$user->save();
```

### Step 8 <a href="#7276" id="7276"></a>

Enable Laravel ERP modules Enable the Laravel ERP modules using the following command:

```
php artisan module:enable
```

### Step 9 <a href="#7535" id="7535"></a>

Run additional Laravel ERP migrations Run the following command to perform additional migrations specific to Laravel ERP:

```
php artisan mybizna:dataprocessor
```

### Step 10 <a href="#80d7" id="80d7"></a>

Generate an application key Generate an application key by running the following command:

```
php artisan key:generate
```

### Step 11 <a href="#b1df" id="b1df"></a>

Start the development server Start the Laravel development server using the following command:

```
php artisan serve
```

open the link http://127.0.0.1:8000/manage

Login using Username: johndoe and Password johndoe
