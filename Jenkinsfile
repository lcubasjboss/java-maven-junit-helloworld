pipeline {
    agent any
    stages {
        stage('Build') {
            steps {            
                checkout scm
                echo "OK Checkout"
                sh '/var/jenkins_home/maven/apache-maven-3.6.0/bin/mvn -B -DskipTests clean package' 
                sh '/var/jenkins_home/maven/apache-maven-3.6.0/bin/mvn -Dmaven.test.failure.ignore=true install'
            }
        }
        
        stage('Test') {
            steps {
                sh '/var/jenkins_home/maven/apache-maven-3.6.0/bin/mvn test'
                echo "Test Complete"
            }
           
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        /*
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
           }
        }*/
    }
}
