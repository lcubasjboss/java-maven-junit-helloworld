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
        
        stage('Unit Test') {
            steps {
                sh '/var/jenkins_home/maven/apache-maven-3.6.0/bin/mvn test'
                echo "Unit Test Complete"
            }
           
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
         stage('Integration Test') {
            steps {
                sh '/var/jenkins_home/maven/apache-maven-3.6.0/bin/mvn verify'
                echo "Integration Test Complete"
            }
           
            post {
                always {
                    junit 'target/failsafe-reports/*.xml'
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
