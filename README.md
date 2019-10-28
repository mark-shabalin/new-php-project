# New PHP project docker-compose template

## Setup

Clone repository into your working space.
Rename folder if needed.

**cd** to the project folder.

Pull source files root directory in *htdocs*.

For example let`s install Wordpress:

`$ wget https://wordpress.org/latest.tar.gz`  
`$ tar -xzf latest.tar.gz`  
`$ cp -a wordpress/. htdocs`  

Now you can remove downloaded Wordpress.

`$ rm -rf wordpress`  
`$ rm latest.tar.gz`  

Next we need to copy *.env.dist* to *.env*.

`$ cp .env.dist .env`  

Please modify variables to your needs.
Edit *COMPOSE_PROJECT_NAME* to name of the project and set database credentials in *.env* file.

## Usage

Now we are ready to start!

`$ docker/up`  

Your project should be available at [http://localhost:8000](http://localhost:8000).
pmpMyAdmin at [http://localhost:8001](http://localhost:8001).

There are useful scripts in *docker* folder:
 * up       builds images, creates containers and starts services
 * php      enters bash promt to *php-fpm* container
 * down     stops services, if started nad deletes containers and networks (*mysql* and *phpmyadmin* volumes are persisted)
 * delete   removes everything, incuding volumes (careful, results database loss)
