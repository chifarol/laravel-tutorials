<!-- @format -->

# Introduction to Eloquent

Eloquent is an **ActiveRecord ORM**

- **ORM** in that it’s a database **abstraction layer** that provides a single interface to interact with multiple database types (MySQL, PostgreSQL, MongoDB)
- **ActiveRecord** in that a **single** Eloquent **Model** class can provide the ability to
  - interact with the table as a whole ( e.g. `User::all()` gets all users, `User::where('name','obi')` ),
    AND
  - also representing an individual table row ( e.g., $sharon = new User() )
- Additionally, each instance is capable of managing its own persistence; you can call `$sharon->save()` or `$sharon->delete()`.

```php
// In a controller
public function save(Request $request)
{
    // Create and save a new contact from user input
 $contact = new Contact();
 $contact->first_name = $request->input('first_name');
 $contact->email = $request->input('email');
 $contact->save();
 return redirect('contacts');
}
```

## Creating and Defining Eloquent Models

- Run the artisan command to create a model
- to automatically create a migration when you create your model, pass the `-m` or `--migration` flag

```php
php artisan make:model Contact
// to automatically create a migration when you create
php artisan make:model Contact --migration
```

### Table name

- The default behavior for table names is that Laravel **snake_cases** and **pluralizes** your class name
  - so **CartItems** Model would access a table named **cart_items**
  - assign a custom table name via `protected $table` property to explicitly specify target table

```php
protected $table = 'contacts_secondary';
```

### Primary key

- Laravel assumes, by default, that each table will have an **autoincrementing intege**r primary key, and it will be named **id**
- change the name of your primary key via `protected $table` property
- And if you want to set it to be nonincrementing, use: `public $incrementing = false`;

```php
protected $primaryKey = 'contact_id';
public $incrementing = false;
```

### Print summmary of Eloquent Model

- As your project grows, it may become a bit challenging to keep track of each model’s
  definition, attributes, and relations.
- The `model:show` command can help with this

```php
// summarize Post
php artisan model:show Post
```

### Timestamps

- Eloquent expects every table to have `created_at` and `updated_at` timestamp columns.
- If your table won’t have them, disable the $timestamps functionality:

```php
public $timestamps = false;
```

- You can customize the format for your timestamps by setting the `$dateFormat` class property to a custom string
- The string will be parsed using PHP’s `date()` syntax

```php
 protected $dateFormat = 'U';
```

## Retrieving Data with Eloquent

- Most of the time when you pull data from your database with Eloquent, you’ll use **static calls** on your Eloquent model

```php
$allContacts = Contact::all();
```

### Chunking responses with chunk()

- makes it possible to break your requests into smaller pieces (chunks) and process them in batches to **save memory**

```php
//  split a query into “chunks” of 100 records each
Contact::chunk(100, function ($contacts) {
 foreach ($contacts as $contact) {
 // Do something with $contact
 }
});
```

## Insert Data with Eloquent

1. `make()`

- creates an instance of the model
- `save()` must be called to save the instance to database

```php
$contact = new Contact;
$contact->name = 'Ken Hirata';
$contact->email = 'ken@hirata.com';
$contact->save();
// or
$contact = new Contact([
  'name' => 'Ken Hirata',
  'email' => 'ken@hirata.com',
]);
$contact->save();
// or
$contact = Contact::make([
  'name' => 'Ken Hirata',
  'email' => 'ken@hirata.com',
]);
$contact->save();
```

2. create()

- to save instance automatically use `create()` method
- every property you set via `Model::create()` has to be approved for “mass assignment” in the Model class `$fillable` property

```php
$contact = Contact::create([
 'name' => 'Keahi Hale',
 'email' => 'halek481@yahoo.com',
]);

// in Models/Contact.php
class Contact extends Model
{
  //  approved for mass assignments
    protected $fillable = [
        'name',
        'email',
    ];
}
```

## Updates

- Updating records looks very similar to inserting.

```php
$contact = Contact::find(1);
$contact->email = 'natalie@parkfamily.com';
$contact->save();
```
