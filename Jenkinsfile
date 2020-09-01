pipeline {
    agent any
    stages {
        stage('Build Docker image') {
        when{
        branch 'master'
        }
            steps {
            Script{
            app=docker.build("dockerhubusername/task")
            app.inside{
            sh 'echo $(curl localhost:8080)'
            }

            }

            }
        }
        stage('push docker image'){
        when{
            branch 'master'
        }
        steps{
        Script:{
            docker.withRegistry('https://registry.hub.docker.com','docker_hub_login'){
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
            }
        }
        }

        }

        stage('Deploy to production'){
                when{
                    branch 'master'
                }
                steps{
                input 'Deploy to production?'
                milestone(1)
                withCredentials([usernamepassword(credentialsId:'webserver_login',usernameVariable:'username' passwordVariable:'Userpass')])

                Script:{
                   sh "sshpass -p $Userpass -V ssh -o StrictHostKey Checking=no $USERNAME@prod_ip\" docker pull <docker_image_name>:${env.BUILD_NUMBER}\" "
                   try{
                    sh "sshpass -p $Userpass -V ssh -o StrictHostKey Checking=no $USERNAME@prod_ip\" docker stop <docker_image_name>\" "
                     sh "sshpass -p $Userpass -V ssh -o StrictHostKey Checking=no $USERNAME@prod_ip\" docker rm <docker_image_name>\" "
                }
                catch(err)
                {
                    echo:'caught error:$err'
                }
                 sh "sshpass -p $Userpass -V ssh -o StrictHostKey Checking=no $USERNAME@prod_ip\" docker run --restart always --name task -p 8080:8080 -d hello/task:${env.BUILD_NUMBER}\" "
                }

                }

    }
}