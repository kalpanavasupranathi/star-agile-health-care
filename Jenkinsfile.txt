pipeline{
    agent any
    stages{
        stage('checkout the code from github'){
            steps{
                 git url: 'https://github.com/StarAgileDevOpsTraining/star-agile-health-care/'
                 echo 'github url checkout'
            }
        }
        stage('codecompile with kalpana'){
            steps{
                echo 'starting compiling'
                sh 'mvn compile'
            }
        }
        stage('codetesting with kalpana'){
            steps{
                sh 'mvn test'
            }
        }
        stage('qa with kalpana'){
            steps{
                sh 'mvn checkstyle:checkstyle'
            }
        }
        stage('package with kalpana'){
            steps{
                sh 'mvn package'
            }
        }
        stage('run dockerfile'){
          steps{
               sh 'docker build -t myimg .'
           }
         }
        stage('port expose'){
            steps{
                sh 'docker run -dt -p 8091:8091 --name c005 myimg'
            }
        }   
    }
}
