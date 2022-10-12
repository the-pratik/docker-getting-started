# Node.js with MongoDB and Docker Demo

Application demo designed to show how Node.js and MongoDB can be run in Docker containers. 
The app uses Mongoose to create a simple database that stores Docker commands and examples. 

Interested in learning more about Docker? Visit https://www.pluralsight.com/courses/docker-web-development to view my Docker for Web Developers course.

### Starting the Application with Docker Containers:

1. Install Docker for Windows or Docker for Mac (If you're on Windows 7 install Docker Toolbox: http://docker.com/toolbox).

2. Open a command prompt.

3. Run the commands listed in `node.dockerfile` (see the comments at the top of the file).

4. Navigate to http://localhost:3000. Use http://192.168.99.100:8080 in your browser to view the site if using Docker toolbox. This assumes that's the IP assigned to VirtualBox - change if needed.


### Starting the Application with Docker Compose

1. Install Docker for Windows or Docker for Mac (If you're on Windows 7 install Docker Toolbox: http://docker.com/toolbox).

2. Open a command prompt at the root of the application's folder.

3. Run `docker-compose build`

4. Run `docker-compose up`

5. Open another command prompt and run `docker ps -a` and note the ID of the Node container

6. Run `docker exec -it <nodeContainerID> sh` (replace <nodeContainerID> with the proper ID) to sh into the container

7. Run `node dbSeeder.js` to seed the MongoDB database

8. Type `exit` to leave the sh session

9. Navigate to http://localhost:3000 (http://192.168.99.100:3000 if using Docker Toolbox) in your browser to view the site. This assumes that's the IP assigned to VirtualBox - change if needed.

10. Run `docker-compose down` to stop the containers and remove them.

## To run the app with Node.js and MongoDB (without Docker):

1. Install and start MongoDB (https://docs.mongodb.com/manual/administration/install-community/).

2. Install the LTS version of Node.js (http://nodejs.org).

3. Open `config/config.development.json` and adjust the host name to your MongoDB server name (`localhost` normally works if you're running locally). 

4. Run `npm install`.

5. Run `node dbSeeder.js` to get the sample data loaded into MongoDB. Exit the command prompt.

6. Run `npm start` to start the server.

7. Navigate to http://localhost:3000 in your browser.



## Custom Commands

1. To use custom template instead of default provided by images `docker run -p 8080:80 -v ${pwd}:/usr/share/nginx/html nginx:alpine`

2. To use volumes to store logs outside the container `docker run -p 8080:80 -v ${pwd}/logs:/var/www/logs (dockerhub-name)/(image-name):(version/tag)`

3. To list containers `docker ps` (for running) / `docker ps -a` (for all)

4. To list images `docker images`

5. To build container `docker build -t nodeapp -f node.dockerfile .` or `docker build -t (dockerhub-name)/(image-name):(version/tag) -f node.dockerfile .`

6. To remove container `docker rm (container id)` and to remove image `docker rmi (image id)`

7. To run image `docker run -p 8080:80 -d (image-name):(version/tag)` or `docker run -p 3000:3000 -d (dockerhub-name)/(image-name):(version/tag)`

8. To stop `docker stop (id)`

9. To get logs `docker logs (id)`

10. To pull `docker pull (image-name):(version/tag)` or `docker pull (dockerhub-name)/(image-name):(version/tag)`

11. To push `docker push (dockerhub-name)/(image-name):(version/tag)`

12. To list volumes `docker volume ls`

## Network Commands

1. Create a network `docker network create --driver bridge isolated_network`

2. List networks `docker network ls`

3. Remove network `docker network rm [network]`

4. Run database container in a network `docker run -d --net=isolated_network --name=[container-name] mongo`

5. Run application container in a network `docker run -d -p 3000:3000 --net=isolated_network --name=nodeapp imageName`

6. Inspect network `docker inspect [container-id]`

## Shell into a Container

`docker exec -it <containerId> sh`

## Extras

1. Create a volume `docker create volume <volumeName>`

2. Add volume to a container at the time of creation `docker run -d -p <cp>:<hp> -v <volumeName>:<containerVolPath> --name <customName> <imageName>`

3. Add volume after creation of container `docker cp <customName>:<containerVolPath> <pathToStoreVolume>`

4. Remove all unused containers `docker system prune`

5. Create a new image from a container’s changes `docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]`
  
6. Create a tar file from image `docker save <imageName> > <tarFileName>.tar`
  
7. Recover image from tar file `docker load -i <tarFileName>.tar`
  
8. Create tar file from container `docker export <customName> > <tarFileName>.tar`
  
9. Recover image from tar file `docker import - <customImageName> < <tarFileName>.tar`
