# <span style="color: Green;">Process to setup MongoDB in Laravel project in Linux machine</span>

## Step 1

###### in <span style="color: blue;">.env</span> file add this for database

    DB_CONNECTION = mongodb
    MONGO_DB_HOST = 127.0.0.1
    MONGO_DB_PORT = 27017
    MONGO_DB_DATABASE = dbname
    MONGO_DB_USERNAME =
    MONGO_DB_PASSWORD =


## Step 2

###### Next we have to add this code for MongoDB connection in  <span style="color: blue;"> config/database.php </span> file add this for database in connection array put mongodb array

    'connections' => [
        ...
        'mongodb' => [
                'driver'   => 'mongodb',
                'host'     => env('MONGO_DB_HOST', 'localhost'),
                'port'     => env('MONGO_DB_PORT', 27017),
                'database' => env('MONGO_DB_DATABASE'),
                'username' => env('MONGO_DB_USERNAME'),
                'password' => env('MONGO_DB_PASSWORD'),
                'options'  => []
            ],

        ]
###### And change default connection mysql to mongodb
    'default' => env('DB_CONNECTION', 'mongodb'),

## Step 3

###### install jenssegers/mongodb package run following command in project
    composer require jenssegers/mongodb
    or
    composer require jenssegers/mongodb:dev-develop 

## Step 4 
###### In <span style="color: blue;">config/app.php </span> file register MongoDB Service Provider
    'providers' => [
        ...
        Jenssegers\Mongodb\MongodbServiceProvider::class,
           ]

## Step 5
###### The final task is , after creating model we need to include 
###### **use Jenssegers\Mongodb\Eloquent\Model as Eloquent** 
###### for example if we create A model Name _**Student**_
    php artisan make:model Student

###### We need to do some changes in _**Student**_ model
    <?php

    namespace App;

    use Illuminate\Database\Eloquent\Model;
    use Jenssegers\Mongodb\Eloquent\Model as Eloquent;

    class Student extends Eloquent
    {
        //
    }

###### That's it . Happy coding :heart:
