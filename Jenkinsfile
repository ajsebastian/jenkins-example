pipeline {
    agent any
    def mvnHome
    stages {
        stage ('Compile Stage') {

            steps {
                mvnHome = tool 'M3'
                if (isUnix()) {
                    sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
                } else {
                    bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
                }
            }
        }

        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'maven_3_5_0') {
                    bat 'mvn test'
                }
            }
        }


        stage ('Deployment Stage') {
            steps{
                junit '**/target/surefire-reports/TEST-*.xml'
                archive '*.jar'
            }

        }
    }
}
