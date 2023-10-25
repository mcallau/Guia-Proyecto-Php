# Guia-Proyecto-Ph

# Preparar el sistema

1.  Actualizar la lista de software de apt
    ```
    sudo apt update
    ```
1.  Instalar curl
    ```
    sudo apt  install curl
    ```
1.  Descargar el script de instalacion de docker
    ```
    curl -fsSL https://get.docker.com -o get-docker.sh
    ```
1. Ejecutar el script de instalacion de docker
    ```
    sudo sh ./get-docker.sh
    ```  
1. Añadir el usuario al grupo docker
    ``` 
    sudo usermod -aG docker manuel
    ```

1. Instalar el VSCode
    ```
    sudo snap install code --classic
    ``` 

1. Instalar y configurar git
    ```
    sudo apt install git
    git config --global user.name mcallau
    git config --global user.email manuel.callau@gmail.com
    ```

# Crear proyecto laravel

1. Crear el proyecto Laravel
    ```
    curl -s https://laravel.build/manflix?with=mysql | bash
    ```
# Poner en marcha el proyecto 

1. (Abrirlo en VSCode) Lanzar la aplicación
    ```
    ./vendor/bin/sail up
    ```

# MVC

Routes -> Controller -> View
            |
            v
          Model
            |
            v
           BBDD

Routes es lo que se pide desde el navegador: http://localhost/films/create
Controller es lo que se ejecuta
    Model es el acceso a la base de datos  (Model === Tabla)
View es lo que se le muestre al usuario

Las rutas se definen en el fichero `routes/web.php`
Los controllers van en la carpeta `app/Http/Controllers`
Las view van en la carpeta `resources/views`

## Routes y controller

Se puede poner una ruta tipo `Route::resource` que es como poner 7 rutas (GET, POST; DELETE, ...)

En esta tabla se puede ver las rutas que añade y los metodos del controller que se ejecutan:
https://laravel.com/docs/10.x/controllers#actions-handled-by-resource-controller

## View

Se crea el fichero `blade.php` y se retornan desde el controller con el metodo `view()`

## Model

Se refiere a las tablas de la base de datos.

Para crear un model, por ejemplo `Film` se ejecuta:
```
./vendor/bin/sail php artisan make:model Film --all
```
https://laravel.com/docs/10.x/eloquent#generating-model-classes

Eso crea varios ficheros:

- El migration `database/migrations/2000202_create_film_table.php` ahí es donde tienes que definir los campos de la tabla (ver https://laravel.com/docs/10.x/migrations#columns)

- El seeder `database/seeders/FilmSeeder.php` ahí es donde se pone que añada unos datos pro defecto. En el método `run()` del `FilmSeeder.php` le dices los datos que quieres que añada.
Luego en el fichero `database/seeders/DatabaseSeeder.php` le dices que ejecute el método `run()` del `FilmSeeder.php`


Para ejecutar los cambios en el servidor MySQL, y que se creen las tablas y se añadan los datos-seed- hay que ejecutar:

```
./vendor/bin/sail php artisan migrate:fresh --seed
```

OJO: el `:fresh` hace que se borre toda la base de datos
