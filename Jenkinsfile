pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "Maven"
    }

    stages {
        stage('Gitcheckout') {
            steps {
                // Get some code from a GitHub repository
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'git_cred', url: 'https://github.com/rantnna/WEB_Maven_Project.git']]])
            }
        }
        stage('build') {
            steps {
                bat 'mvn clean install'
            }
        }
        stage('codequality') {
            steps {
                bat 'mvn clean install sonar:sonar -Dsonar.login=admin -Dsonar.password=pipurosy'
            }
        }
        stage('deploy') {
            steps {
                deploy adapters: [tomcat9(credentialsId: '58138457-2109-4db4-80df-278a47912c3d', path: '', url: 'http://localhost:7000')], contextPath: 'webappPiProject4', war: '**/*.war'
            }
        }
    }
}