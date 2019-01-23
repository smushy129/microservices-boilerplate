# High Level Architecture

This project uses `microservice architecture`, where each service is listed under `/services`. Additionally, it makes use of containerization with [Docker](https://www.docker.com/) so that `dev` and `prod` environments are as similar as possible.
Each service has its own Dockerfiles for `dev`, `staging`, and `prod`

The backend is [Flask](http://flask.pocoo.org/) and the client is `React` using [create-react-app](https://github.com/facebook/create-react-app)
DB is [Postgresql](https://www.postgresql.org/)
Auth is done with [JWT](https://jwt.io/)

### CI

I chose to use [TravisCI](https://travis-ci.org/) because its easy. Configure this in `travis.yml`

### Hosting:

Because we decided to host on AWS, we have to use ECS and ECR to manage our container images: [More Info](https://docs.aws.amazon.com/AmazonECR/latest/userguide/ECR_on_ECS.html)
This is configured in `docker-push.sh`. This will push your docker container to ECR. If we decide not to use AWS and use something else like Azure/GoogleCloud, then all we have to do is swap this file.

### To be done:

1. Use [RDS](https://aws.amazon.com/rds/) instead of running db instances in a EC2 instance. We still need a db service in the repo for development, but for staging and prod, we should be using an RDS
2. Figure out why sessions persisted on new tabs (something to do with jwts)
3. more things

### To run locally

_Dependencies Required_

1. Download and install [Docker](https://docs.docker.com/compose/install/)
   Run these commands to verify you successfully installed
   - docker -v
   - docker-compose -v
   - docker-machine -v

2) Download and install [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
   This is needed to run docker

_To start dev environment_

1. Navigate to `services/client` and run `npm install`
2. In your terminal, run `docker-machine create --driver virtualbox default`
3. Run `eval $(docker-machine env default)` after the docker-machine is done building
4. Run `docker-machine ls` and copy the address of the default running docker machine
5. In the root dir, CHANGE the field `REACT_APP_USERS_SERVICE` to the ip address you copied
6. Still within root dir of the project, run `docker-compose -f docker-compose-dev.yml build` to build the project
7. Still within the root dir, run `docker-compose -f docker-compose-dev.yml up -d` to start the container
8. Navigate to the address of your docker machine in your browser to see the running app

_FAQ_

1. `Error with pre-create check: "failure getting a version tag from the Github API response (are you getting rate limited by Github?)`
   Try this https://github.com/docker/machine/issues/3210#issuecomment-203227523
