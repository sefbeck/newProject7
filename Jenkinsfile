pipeline {
    agent any

    stages {
        stage('Gitcheckout') {
            steps {
                git branch: 'main', url: 'https://github.com/sefbeck/newProject7.git'
            }
        }
        
        stage('Test') {
            steps {
                sh 'cd SampleWebApp && mvn test'
            }
        }
        stage('Build Maven') {
            steps {
                 sh 'cd SampleWebApp && mvn package'
            }
        }
        stage('Deploy to Jfrog') {
            steps {
                rtUpload (
                   serverId: 'my-jfrog',
                   spec: '''{
                       "files": [
                           {
                           "pattern": "**/*.war",
                           "target": "my-repo/"
                           }
                        ]
                    }''',
                )    
            }
        }
        
        stage('Deploy to Tomcat') {
            steps {
               deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://54.172.145.169:8080/')], contextPath: 'default', war: '**/*.war'
            }
        }
    }
}
