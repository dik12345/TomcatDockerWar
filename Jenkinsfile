pipeline {
     agent any
     stages {
          stage("Compile") {
               steps {
                    sh "/usr/share/maven compile"
               }
          }
          stage("Unit test") {
               steps {
                    sh "/usr/share/maven test"
               }
          }
     
    
stage("Package") {
     steps {
          sh "/usr/share/maven package"
     }
}
stage("Docker build") {
     steps {
      
          sh "docker build -t deepak_tomcat ."
     }
}

stage("Deploy to staging") {
     steps {
          
          sh "docker stop \$(docker ps -qa)"
          sh "docker rm \$(docker ps -qa)"
          sh "docker run -d -it -v /var/lib/jenkins/workspace/Dockerwebpipeline/target/:/usr/local/tomcat/webapps/ -p 8091:8080 --name Testtomcat deepak_tomcat"
     }
}

     }
  post {
     always {
          sh "echo 'I did It'"
     }
}
}
