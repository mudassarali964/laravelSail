<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo"></a></p>

<p align="center">
<a href="https://github.com/laravel/framework/actions"><img src="https://github.com/laravel/framework/workflows/tests/badge.svg" alt="Build Status"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/dt/laravel/framework" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/v/laravel/framework" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/l/laravel/framework" alt="License"></a>
</p>

## Laravel Sail

[Laravel Sail](https://laravel.com/docs/10.x/sail#introduction) is a light-weight command-line interface for interacting with Laravel's default Docker development environment. Sail provides a great starting point for building a Laravel application using PHP, MySQL, and Redis without requiring prior Docker experience.

At its heart, Sail is the docker-compose.yml file and the sail script that is stored at the root of your project. The sail script provides a CLI with convenient methods for interacting with the Docker containers defined by the docker-compose.yml file.

## Steps to run the project with docker through the sail

- 1- Create new file as .env in the root directory, copy .env.example file code into .env file and replace the Database setting as:
    
    - DB_CONNECTION=mysql
    - DB_HOST=mysql
    - DB_PORT=3306
    - DB_DATABASE=laravel_cashier
    - DB_USERNAME=root
    - DB_PASSWORD=

- 2- Make sure Docker Desktop is running on your machine.
- 3- Add your project into docker FILE SHARING: Go to docker setting -> Resources -> FILE SHARING -> Add your project path 
    -> Apply and restart.
- 4- Run the command to install the composer: composer install
- 5- Configuring A Shell Alias
    - [Configuring A Shell Alias](https://laravel.com/docs/10.x/sail#configuring-a-shell-alias).
    - To make sure this is always available, you may add this to your shell configuration file in your home directory, such as ~/. zshrc or ~/.bashrc, and then restart your shell.
    - Steps for configuring the alias: 
        - if you are using bash run in your terminal then run the follwing commands:
        - Run this command: nano ~/.bash_profile
        - Add alias into the file and save the file:
        - alias sail='[ -f sail ] && bash sail || bash vendor/bin/sail'
        - Finally run this command: source ~/.bash_profile 
    - If successfully configured then run the following commands to start the docker
        - sail build --no-cache
        - sail up -d
        - sail artisan key:generate
        - sail artisan migrate:fresh --seed
    - If error in configuration then move to the next step (without alias)

- 6- If any case step "5" get failed, then do the following steps: (without alias setup)
    - ./vendor/bin/sail build --no-cache
    - ./vendor/bin/sail up -d
    - ./vendor/bin/sail artisan key:generate
    - ./vendor/bin/sail artisan migrate:fresh --seed

## Run the project in the docker via sail (Alias Configuration)

- sail build --no-cache
- sail up -d
- sail artisan key:generate
- sail artisan migrate:fresh --seed

## Run the project in the docker via sail (No Alias Configuration)

- ./vendor/bin/sail build --no-cache
- ./vendor/bin/sail up -d
- ./vendor/bin/sail artisan key:generate
- ./vendor/bin/sail artisan migrate:fresh --seed

## Stop the project in the docker via sail (Alias Configuration)

- sail stop
- sail down

## Stop the project in the docker via sail (No Alias Configuration)

- ./vendor/bin/sail stop
- ./vendor/bin/sail down

## Only for update the database credentials from env

- If we need to change the database credentials from .env file, then we should follow the given steps:

- 1- Run the given commands:
	sail stop
	sail down => Will untagged (not remove), all the images and volume related to the container
	sail down -v => Will remove all the containers volume

- 2- Manually removed all the images related to the container
- 3- Then change the database credentials in the .env file
- 3- Finally Run these commands:
	- sail build --no-cache OR ./vendor/bin/sail --no-cache
	- sail up -d OR ./vendor/bin/sail up -d
	
