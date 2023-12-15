pipeline {
    agent any
    
    tools {
        nodejs "nodejs"
    }
    environment {
        PUBLIC_URL       = 'https://satriadiouf24.github.io/Capstone_Project'
        GIT_CREDENTIALS= credentials('jenkins-github-token')
        GITHUB_REPOSITORY = 'satriadiouf24/capstoneproject'
    }
    stages {
        stage('Checkout') {
      steps {
        script {
          checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/Satriadiouf24/capstoneproject', credentialsId: GIT_CREDENTIALS]]])
        }
      }
    }
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        
        stage('Test') {
            steps {
            sh 'chmod +x ./jenkins/scripts/test.sh'
               sh './jenkins/scripts/test.sh'
            }
        }
           
        stage('Deploy') {
            steps {
                sh 'chmod +x ./jenkins/scripts/deliver.sh'
                sh 'chmod +x ./jenkins/scripts/kill.sh'
                sh './jenkins/scripts/deliver.sh'
                sh './jenkins/scripts/kill.sh'
                echo'Tahapan deploy ke Github Pages'
                //Dengan beberapa Konfigurasi seperti Credential pada github (jenkins-github-token)
                sh 'chmod +x ./jenkins/scripts/github-pages.sh && ./jenkins/scripts/github-pages.sh'
            }
        }
    }
}
