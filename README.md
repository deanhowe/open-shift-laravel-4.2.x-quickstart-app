## [ :: NOT REALLY FOR INTERNET CONSUMPTION :: ]
~~ *use at your own risk* ~~ 

A Laravel 4.2.* QuickStart App for running on OpenShift
=======================================

Really this repo is just a few files `.openshift/action_hooks/build` && `.openshift/action_hooks/deploy`. Strictyly speaking I don't know if the `.openshift/action_hooks/post_deploy` is needed, but I needed it inside Origin.

There are some Laravel files in `.openshift/misc` that are worth looking at.

##Howto Use this QuickStart

Create a new application from the PHP 5.4 Cartridge, adding MySQL 5.5 and setting [this repo](https://github.com/deanhowe/open-shift-laravel-4.2.x-quickstart-app) as the 'Optional URL' under'SourceCode'. Set 'scaling' now - because I think it's hard to update after the initial creation of the application.

Or run the following to use rhc in the terminal

    rhc app create -a <app-name> --from-code https://github.com/deanhowe/open-shift-laravel-4.2.x-quickstart-app php-5.4 mysql-5.5 --scaling

This might take a while, it's downloading Laravel (about 25MB). 

I'm going to assume you have the Laravel Installer installed locally, in which case run this...

    laravel new laravel
    
Wait for that to download/install and then...
    
    cd laravel && mv ./* ../ && mv ./.git* ../ && cd ../ & rm -fr laravel
    
Check the git repo status with `git status`.

Add the new files to the git repo…

    git add CONTRIBUTING.md app artisan bootstrap composer.json phpunit.xml readme.md server.php public
    
Then git push
    
    git push
  
## What the scripts actually do…
  
### Build

 * Updates composer to the latest version & creates a bash alias to it
 * Installs Laravel into `OPENSHIFT_BUILD_DEPENDENCIES_DIR`
 * Updates your `~/.bash_profile` on the server to make things a little more friendly...

 
### Deploy

 * Link the vendor directory from the build dependancies into the repo
 * Updates your `./app/config/*` files to use any config files in `.openshift/misc/config/*`
 * Allows you to run Artisan commands listed in a marker file `.openshift/markers/artisan`

