pipeline{
    tools {
        maven 'Maven3'
    }
    agent any
    environment {
        registry = "923770093922.dkr.ecr.us-east-1.amazonaws.com/myrepo"
    }
    stages{
        stage('git clone'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', url: 'https://github.com/sarithabora2246/mynewspringbootapp.git']]])
            }
        }
        stage('Build'){
            steps{
                sh 'mvn clean install'
            }
        }
        stage('Unit test'){
            steps{
                echo '<--------------- Unit Testing started  --------------->'
                sh 'mvn surefire-report:report'
                echo '<------------- Unit Testing stopped  --------------->'
            }
        }
        stage('Sonarqube Analysis'){
                environment {
                    scannerHome = tool 'sonar-scanner'
                }
                steps{
                    echo '<----------- Sonarqube Analysis started'
                    withSonarQubeEnv('sonar-cloud') {
            sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=springbootapp -Dsonar.organization=mypractice -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=0e9c72ff9c9ffecc5d0fc09167bad472ec394b9d'
                    echo '<----------- Sonarqube Analysis End'
                }
            }
        }
    }
}