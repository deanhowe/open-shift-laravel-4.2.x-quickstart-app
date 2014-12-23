## [ :: NOT REALLY FOR INTERNET CONSUMPTION :: ]
~~ *use at your own risk* ~~ 

A Laravel 4.2.* QuickStart App for running on OpenShift
=======================================

Really this repo is just a few files `.openshift/action_hooks/build` && `.openshift/action_hooks/deploy`. Strictyly speaking I don't know if the `.openshift/action_hooks/post_deploy` is needed, but I needed it inside Origin.

There are some Laravel files in `.openshift/misc` that are worth looking at.


### Build

 * Updates composer to the latest version & creates a bash alias to it
 * Installs Laravel into `OPENSHIFT_BUILD_DEPENDENCIES_DIR`
 * Updates your `~/.bash_profile` on the server to make things a little more friendly...

 
### Deploy

 * Link the vendor directory from the build dependancies into the repo
 * Updates your `./app/config/*` files to use any config files in `.openshift/misc/config/*`
 * Allows you to run Artisan commands listed in a marker file `.openshift/markers/artisan`

