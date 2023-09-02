                                      ---------------------------------
                                      <<<<<<<    PHP Artisan    >>>>>>>
                                      ---------------------------------
- php artisan serve >> launching the application.
- php artisan -V >> getting the version of laravel.
- php artisan make:model model_name -mc >> will make a model, migration file and controller.
- Creating migration >> php artisan make:migration name [--create='table_name'] //Making a migration and populate it with a table .. if --create flag isn't added it will be empty migration.
- php artisan migrate:refresh >> rollback all the migrations and installs it again. #Caution : It removes all your data. 
- php artisan migrate:rollback >> rollback all migrations.
- php artisan migrate >> installs all not-installed migration.
- Using "php artisan migrate:reset" >> removes all the tables that is created with the migrations scripts
- Using "php artisan tinker" >> opens the command line for the php "Shell"
============================================================================================================
                                        -----------------------------
                                        <<<<<<<    Routing    >>>>>>>
                                        -----------------------------                                        
//Routing with url and a closure
- Route::get('[/]route_name/{id}', function($id){
    //use the variable
    return view('template_name');
  });

//Routing with url and a controller method
- Route::get('[/]route_name', 'controller_name@Method_name');
  # Note: You can use any variable name for the route url but make sure that the sequence of the variables is correct.

//Naming the route.
- Route::get('/','Controller@verb')->name('Route_name'); //Giving a specific name to the route so that you can redirect to it directly.

//Model Route Binding
- Rturning an object in the method referenced by its primary key in the route
  Route::get('/tasks/{variable}', function(Class $variable){
    // Use $variable
  });
  # Note: the variable name in the route definition must be like the variable name in the controller method.

- Be aware when routing with a variable firstly then routing statically with two layers .. 'post/{id}' will be like 'post/add'
============================================================================================================
                                  -------------------------------------------
                                  <<<<<<<    Blade Template Engine    >>>>>>>
                                  -------------------------------------------                                    
- Blade view files use the .blade.php file extension and are typically stored in the resources/views directory.
- You can use basic layout files to be the basic structure of your view and put @yield('section') into it to declare places that another sections can be injected in it.
- We entends a layout in a template using @extends('master_file_name'); .. Then we declare sections to fill the places that we declared it first.
- We declare a new section using
- Using @section('section_name') to declare a new section and we end it with @stop or @endsection.
- You can use @include('segment') to include it directly to the current template.
- {{ $variable }} >> echo $variable
- @foreach($tasks as task) ..... @endforeach
- @if(CONDITION) .... @else .... @endif
- You can use RESTful requests like patch, put, delete in a form with using {{ request_field('request_type') }} in the form.
- You must use a CSRF protection field in any form. Use {{ csrf_field() }} in the form.
============================================================================================================
                                      ---------------------------------
                                      <<<<<<<    Controllers    >>>>>>>
                                      ---------------------------------                                        
// Redirecting
- return redirect('/path/to/redirect');
- return redirect()->route('route_name');
- You can redirect with custom error using  redirect()->withErrors( [ 'message' => 'Custom error' ] )

// Returning a view
- return view('template');
- return View::make('template');

//Returning a view with a variable
- return view('bisho', ['name' => 'Value', ...]); 
- return view('bisho')->with('variable_name', 'Value');

//Using Forms
- You access fields from the request using request()->Field_name.

//Mass Assignment
- You must add the fields that you want to insert from a form in the model. 
- $guarded = ['All the variables that cannot be added through a form to this model table']
- Or $fillable = [' All the variables that can be added to this mdoel table']

//Validation
- Use $this->validate($request, 'Rules');
- $this->validate($requset, [
    'body' => 'required',
    'title' => 'required'
    'email' => 'required|unique:table_name' //The column name in the table must be as the field name.
  ]); //Example
- To catch errors from validation, there is an object injected in each view called 'errors' and to get all the erros as an array we call '$errors->all()'
- To keep the old input in the field we call the method 'old('field_name')' in the text area field. // It's put as a default value of each field and will automatically return NULL if there is no validation errors.

//Middleware
- You can apply middleware to a custom functions in your Controller using $this->middleware('guest', ['except' => 'specific_method']);
============================================================================================================
                                      ----------------------------------
                                      <<<<<<<    Global Notes    >>>>>>>
                                      ----------------------------------
// Migrations
- We define a migration table field using $table->field_type('field_name');
- Fields Type integer, increments, text "long", string "small", timestamps. //More in the Docs.
- Use $table->field_type('column_name')->default($Value); //Adding a default value for the table column
- Default timestamps columns defining fields of Carbon Instances for each created_at and updated_at. //Carbon is a library that deals with timestamps.
- Note: If any migration is deleted, you will get an error from the composer autoloader because it tries to autoload a file that doesn't exist ... So we must use "composer dump-autoload". It clears the autoload cache.

//Namespace
- Any Class must be namespaced at the top of the file if you want to use it directly without its namespace.
- "use App\Model" >> will include the class direclty to use it. Or use App\Model in each class usage.
- There is Global classes like Session and Auth. It's included using "use Auth;" only.

//Query Builder
- DB::table('posts')->get( [array_of_specific_columns] )->where('title', 'Hi there')->where(another_condition)->first();
- DB::table('posts')->insert( [array_of_key_values_pairs] );
- DB::table('posts')->where(condition)->delete();
- ->where('#1', '> | >= | < | <=', '#2');

//Service providers
- Located at app/Providers/AppServiceProviders.php
- You can add a View::composer('view', closure); //triggers the closure each time the view is loaded
  view()->composer('layouts.sidebar', function($view){
    $view->with('variable_name', 'value');
  }); //Example for view composers

- When retuning the controller method with a sql object it converts it automatically into json.
- There is a secure file called .env so we can put any passwords in it.
============================================================================================================
                                      ----------------------------------
                                      <<<<<<<    Elequent ORM    >>>>>>>
                                      ----------------------------------
//Adding records
- Model::create(['field#1' => value#1, 'field#2' => value#2]); //Adding a new record to the table associated with the model.
- Model::create($request->all()); //Quick example.
- Creating an object and populate it with the data required then use '$object->save()';

//Quering 
- Model::all() //Returns all model records.
- Model::SelectRaw('id, name, another_specific_column'); //Selecting columns like pure mysql.

//Deleting
- get the record that you need as elequent builder object then use '$object->delete()'.
- Don't transform the builder object into collection object using 'builder_object->get()' before deleting.

//Query Scope
- Used to make a specific query condition or filtering as a separate function. You must use 'scope' prefix before function declaration.
  public function scopeIsComplete($query, $other_parameters)
  {
    $query->where(SPECIFIC_CONDITION);
  } //Example

//One to many relationships
- In the one side, Make a function called the name of the other side column and return $this->hasMany('\App\Many_Model');
- In the many side, Make a function called the name of the other side column and return $this->belongsTo('\App\One_Model');
  public function posts(){
    return $this->belongsTo('\App\User');
  } //Each user has many posts.
  public function user(){
    return $this->hasMany('\App\Post');
  } //Each post belongs to a user.
  $post->user //Get the user object of this post.

//Elequent methods
- Model::where('id', '>=', 1) //Getting a builder object have a specific condition.
- Use $builer_object->get() to transform it to collection object 'Array of objects'.
- Model::Latest(); //Return all the records in descinding order.
- ToArray() --> turning object results into array.
- OrderByRaw('month, year') //Getting results ordered by a specific rows.
- GroupBy('field_name');
- Model::pluck('column_name'); //Getting a collection with only the column specified.
- Model::with(['comments.user', 'user']) //Getting a builder object with all posts, user of each post, comments and user of each comment.
- $collection_object->load(['comments.user', 'user']) //Loading the collection object user, its comments and the user of each comment.
- WhereYear('created_at | updated_at', 'Year')   //Returns builder object where the year in timestamp equals to a specific year.
- WhereMonth('created_at | updated_at', 'month') //Returns builder object where the month in timestamp equals to a specific month.
- ```DB::enableQueryLog()``` saves all the queries made to the database in a log file that you can access using ```DB::getQueryLog()```. This is a very useful tool when debugging and optimizing queries.

============================================================================================================
                                          -----------------------------
                                          <<<<<<<    Waiting    >>>>>>>
                                          -----------------------------
- Service Providers

## Service "IoC" "Dependency Injection" Containers



## Facades

- A facade is a pattern that uses a class wrapping a complex library to provide a simpler and more readable interface to it.
- Laravel facades serve as "static proxies" to underlying classes in the service container
- Every service inside the container has a unique name. In a Laravel application, to access a service directly from the container, we can use the ```App::make()``` method or the ```app()``` helper function.
- someService::methodName();
- Laravel Facade can invoke methods from the services in the container in a more-readable way using ServiceName::methodToBeInvoked.
- The ```Facade``` base class has a private property named ```$app``` which stores a reference to the service container.
- Inside the base facade class, the ```__callStatic``` magic method has been implemented to handle calling of static methods which don’t actually exist.
