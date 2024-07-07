<!-- @format -->

## Configuration

- core settings of your Laravel application live inside the config folder
- this includes settings for database connection settings, queue
  and mail settings, etc
- Each of these files **returns** a PHP **array**
- Each value in the array is accessible by a config key ( that is comprised of the filename and all descendant keys, separated by dots "." )

```php
// config/services.php

return [
 'sparkpost' => [
 'secret' => 'abcdefg',
 ],
];

```

to access that config variable use

```php
 config('services.sparkpost.secret');
```
