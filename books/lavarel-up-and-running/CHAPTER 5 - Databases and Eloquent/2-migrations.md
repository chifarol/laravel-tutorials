<!-- @format -->

## Migrations

A single migration file that defines 2 things:

1. modifications desired when running this migration **up**
2. modifications desired when running this migration **down**

### Creating a migration

- a new migration file is created with `php artisan make:migration`
- The default format for targeting a table is `create_{{ table_name_goes_here }}_table`
- Use the `--table=table_name` flag to specify the target table if you want a custom migration filename
- Use `--create=table_name` prefill the migration with code designed to create a table
- Migrations are always run in order by date that's why every migration filename has a date stamp e.g **2018_10_12_000000_create_users_table.php**

```php
// create new migration file for "users" table
php artisan make:migration create_users_table
// using --table to specify the target table
php artisan make:migration add_votes_to_users_table --table=users
// prefill the migration with code designed to create a table
php artisan make:migration create_users_table --create=users
```

### “Up” and “Down” in Migrations

- When php artisan migrate is called for the **first time**, the system grabs **each** migration, starting at the oldest date, and runs its **up()** method
- But since the migration system also allows you to “undo” your most recent set of migrations, It’ll grab each of them and run its **down()** method
