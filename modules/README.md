# Modules

Mybizna modules are developed using the Laravel-modules package.

Laravel-modules is a popular package for Laravel that provides a modular architecture for creating web applications. It allows developers to create self-contained modules in Laravel. This package is developed and maintained by Nicolas Widart.

One benefit of using Laravel-modules is reusable code that can be installed or uninstalled without affecting the system . This makes it easy to manage and update each module separately.

Mybizna Module works with the following file structure by minimum.

```

Modules/
  ├── Blog/    
      ├── Entities/
          ├── Data/
              ├── Blog.php          // Preset Data for ERP
          ├── Blog.php              // Entity 
      ├──views/
          ├── admin/
              ├── blog/
                  ├── form.vue
                  ├── search.vue
                  ├── list.vue
      ├── Tests/
      ├── composer.json
      ├── module.json
```

Note Entites is auto-migrated using the command or after the composer version is changed to a new version.

```
php artisan automigrator:migrate
```

Other module functions can be added as illustrated in [https://nwidart.com/laravel-modules/v6/introduction](https://nwidart.com/laravel-modules/v6/introduction)
