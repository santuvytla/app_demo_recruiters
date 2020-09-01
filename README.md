# Task Completion Steps for Reviewer

This is a simple app written using nodejs. it has details of execution of task

## Running the app without docker

You need a Java JDK 7 and Nodejs v14.8.0 or later to run the build. You can run the build like this:

    npm install

You can run the app with:

    npm start

Once it is running, you can access it in a browser at http://localhost:8080
http://localhost:8080/healthcheck to get the health status of the app
In additional to the given healthcheck example its needed to know the nodejs version for campatibility,uptime for the time the server is running,app build version and port in case you use domain so that port is not visible(example use is when app is behind an ALB in aws).
We can change the path in the app.js file if needed.

##Running the app with docker
You need a Java JDK 7 and Nodejs v14.8.0 or later to run the build. You can run the build like this:

    docker --version      (to verify wheather docker is installed)
    sudo docker build -t <name>/task . (to build the image the name should be dockerhub username for best practise)
    
You can run the app with:

    sudo docker run -p 8080:8080 -d <name>/task
    sudo docker ps    (to verify the process)

Once it is running, you can access it in a browser at http://localhost:8080

Finally Automating the build process(jenkins file is also present in folder):
	step1:	we are here using the jenkins for build and deploying to the production server.
we provide the credentials of dockerhub and github account in the credentials tab.
	step2:  create item of multibranch pipeline item (which has both production and development branches)
	step3:Now everything is linked click build now.The CI/CD pipeline is implemented.

NOTE:We should change the name of docker image in Jenkins file also prod server ip,credentials and other secretive data based on requirements..jenkins is password protected and access can be controlled based on userIP.

Thank you for reading!!!..plzz contact if any queries
	 
		
		
