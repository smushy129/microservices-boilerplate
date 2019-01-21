#High Level Architecture

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

1. Install [Docker](https://docs.docker.com/compose/install/)
2. more steps to come
