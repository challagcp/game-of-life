pipeline {
    agent { label 'ltecomm'}
    triggers {
        cron('H * * * 1-5')
    }
    parameters {
        string(name: 'MAVENGOAL', defaultValue: 'clean package', description: 'Enter your maven goal')
    }
    stages {
        stage('scm') {
            steps {
                git 'https://github.com/challagcp/game-of-life.git'        
            }
        }
        stage('build') {
            steps {
                sh script: "mvn ${params.MAVENGOAL}"
            }
        }
        stage('post build') {
            steps {
                junit 'gameoflife-web/target/surefire-reports/*.xml'
                archiveArtifacts 'gameoflife-web/target/*.war'
            }
        }
    }
}
