pipeline {
    agent any
    stages {
     //   stage('Stage-0 : Static Code Analysis Using SonarQube') { 
       //     steps {
    //           sh 'mvn clean verify sonar:sonar -DskipTests'
     //       }
       // }
        stage('checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Thabrezmd/Deploy_java_app_tomcat.git']]])
            }
        }        
        stage('Clean') {
            steps {
               sh "mvn -Dmaven.test.failure.ignore=true clean"
            }
        }
        
        stage('Validate') {
            steps {
                sh "mvn validate"
            }
        }
        
        stage('Compile') {
            steps {
                sh ('mvn compile');
            }
        }
        
        stage('Test') {
            steps {
                sh ('mvn test');
            }
        }
        
        stage('Package') {
            steps {
                sh ('mvn package');
            }
        }
        
        stage('Verify') {
            steps {
                sh ('mvn verify');
            }
        }
        
        stage('Install') {
            steps {
                sh ('mvn install');
            }
        }
            
         stage('Stage-9 : Deployment - Deploy a Artifact devops-3.0.0-SNAPSHOT.war file to Tomcat Server') { 
            steps {
                sh 'curl -u thabrez:thabrezmd -T target/**.war "http://3.110.87.198:8080/manager/text/deploy?path=/maven&update=true"'
            }
        } 
  
          stage('Stage-10 : SmokeTest') { 
            steps {
                sh 'curl --retry-delay 10 --retry 5 "http://3.110.87.198:8080/maven"'
            }
        }
        }
          
    }
