pipeline{
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
        //stage('Sonarqube Analysis'){
                //environment {
                    //scannerHome = tool 'sonar-scanner'
               // }
                //steps{
                   // echo '<----------- Sonarqube Analysis started'
                    //withSonarQubeEnv('sonar-cloud') {
            //sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=sarithapipelineproject -Dsonar.organization=sarithapipelineproject -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=010543b78e4cb68d08f3ed9640c1fa6046e9abe7'
                    //echo '<----------- Sonarqube Analysis End'
                //}
            //}
        //}
    }
}
