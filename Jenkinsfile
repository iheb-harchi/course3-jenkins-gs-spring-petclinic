pipeline {
    agent any
    stages {
        stage("checkout") {
            steps {
                git branch: 'main', url: 'https://github.com/iheb-harchi/course3-jenkins-gs-spring-petclinic.git'
            }
        }
        stage("build") {
            steps {
                 sh "./mvnw package"
            }
        }
        stage("capture") {
            steps {
                archiveArtifacts '**/target/*.jar'
                junit '**/target/surefire-reports/TEST*.xml'    
            }
        }    
    }
   post {
        always {
            emailext(
                subject: "${currentBuild.currentResult}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                body: """Build URL: ${env.BUILD_URL}
Result: ${currentBuild.currentResult}
Build Log: ${currentBuild.absoluteUrl}console""",
                recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                to: 'always@foo.com'
            )
        }
    }
}
    
