# OLA-HD: A Long-term Archive System
OLA-HD is a mixture between an archive system and a repository.
The input is a `.zip` file whose content is structured as [BagIt](https://tools.ietf.org/html/rfc8493 "BagIt RFC").
The zip content will be validated before any further actions take place.
Data uploaded to the system will be stored in both tapes and hard drives.
The separation rules are defined in the configuration file.
In addition, each uploaded zip gets a persistent identifier (PID).
This PID can be used for sharing, citing, and versioning purposes.

If you deploy your own instance, a [Swagger](https://swagger.io/ "Swagger homepage") documentation is
available at `/swagger-ui.html`.

For the prototype:
* Please click [here](http://ola-hd.gwdg.de/ "OLA-HD Prototype") to experience it.
* Please click [here](http://ola-hd.gwdg.de/api/swagger-ui.html "OLA-HD API Documentation") for the current Swagger documentation.

## Repositories
Besides this repository, OLA-HD consists of 3 repositiories:

[Backend](https://github.com/subugoe/olahd_backend): RESTful Service  
[User-GUI](https://github.com/subugoe/olahd_user_frontend): web UI for public usage  
[Admin-GUI](https://github.com/subugoe/olahd_admin_frontend): web UI for logged in users  


## Project structure
```
.
├── .gitlab
│   └── issue_templates  -> templates used by Gitlab when users want to create issues
├── images               -> images used in README files
├── nginx                -> the Nginx proxy for the whole system
├── .env                 -> environment variables for all Docker images
├── .gitignore
├── LICENSE
├── README.md
├── build.sh             -> run this file to build the Docker image and start up the whole system (database, back-end, front-end, reverse proxy)
└── docker-compose.yml   -> describe all images in the system
```

## Prerequisites
* [Docker](https://docs.docker.com/install/ "Docker installation guide")
* [docker-compose](https://docs.docker.com/compose/install/ "docker-compose installation guide")

## Install and run
```
git clone https://github.com/subugoe/olahd_deployment
cd olahd_deployment
git clone https://github.com/subugoe/olahd_backend
git clone https://github.com/subugoe/olahd_user_frontend
git clone https://github.com/subugoe/olahd_admin_frontend
./build.sh
```

## System overview
![System overview](/images/overview.png?raw=true "System overview")

All requests go first to the Nginx proxy.
Depending on the URL path, it will either forward the request to the back-end service, or serves static HTML files.
As depicted in the image, there are four components: Nginx, back-end, front-end for normal user, and front-end for admin.
