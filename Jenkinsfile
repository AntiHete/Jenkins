pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/AntiHete/Jenkins.git', credentialsId: '033e015d-f51b-4ae1-8cf7-09fe320c5d0d'
            }
        }
        
        stage('Build') {
            steps {
                // Крок для збірки проекту з Visual Studio
                // Встановіть правильні шляхи до рішення/проекту та параметри MSBuild
                bat '"C:/Program Files/Microsoft Visual Studio/2022/Community/MSBuild/Current/Bin/MSBuild.exe" test_repos.sln /t:Build /p:Configuration=Release'
            }
        }

        stage('Test') {
            steps {
                // Команди для запуску тестів
                bat "x64\\Release\\test_repos.exe --gtest_output=xml:test_report.xml"
            }
        }
    }

    post {
    always {
        junit 'test_report.xml'
    }
}
}