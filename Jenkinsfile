pipeline {
    agent any
    stages {
        stage ('Compile Stage') {
            steps {
               bat(/"M3\bin\mvn" -Dmaven.test.failure.ignore clean package/)
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
