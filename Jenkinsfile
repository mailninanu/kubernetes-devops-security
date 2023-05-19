pipeline {
  agent any

  stages {
      stage('Build Artifact') {
            steps {
              sh "mvn clean package -DskipTests=true"
              archive 'target/*.jar'
            }
      }

       stage('Unit Tests - Junit and Jacoco') {
                    steps {
                      sh "mvn test"
                    }
                    post{
                        always{
                            junit 'target/surefire-reports/*.xml'
                            jacoco execPattern: 'target/jacoco.exec'
                        }
                    }
       }
        stage('Docker image build and push') {
                    steps {
                     // withDockerRegistry([credentialsId: 'docker-hub', url:]){
                      sh 'printenv'
                      sh 'docker build -t ninanu/numeric-app'
                      //sh 'docker push ninanu/numeric-app:""$GIT_COMMIT""'
                       //}
                     }
        }

  }
}