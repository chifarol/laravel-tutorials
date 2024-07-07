<!-- @format -->

# Laravel Setup

---

Laravel offers 5 tools for local development:

- Artisan serve,
- Sail,
- Valet,
- Herd, and
- Homestead.

## Steps (using Artisan)

1.  Installing lavarel
    There are 2 ways of "installing" up laravel

    - Installing Laravel with the Laravel Installer Tool

      - composer global require "laravel/installer"
      - laravel new projectName

              OR

    - Installing Laravel with Composer’s create-project Feature
      - composer create-project laravel/laravel projectName

2.  Install dependencies

    - composer install
    - composer dump-autoload (this is usually done automatically by composer)

3.  install npm modules

    - npm install

4.  run npm

    - npm run dev

5.  make a copy of the sample .env.example to a .env file

    - cp .env.example .env

6.  generate encryption key to avoid "No application encryption key has been specified." error

    - php artisan key:generate

7.  Link storage

    - php artisan storage:link

8.  Run server
    - php artisan serve
