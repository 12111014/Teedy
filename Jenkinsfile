pipeline {
      agent any
      stages {
        stage('Build') {
          steps {
             sh 'mvn -B -DskipTests clean package'
          }
         }

        stage('Generate Javadoc') {
            steps {
                sh 'mvn javadoc:jar'
            }
        }

      stage('Generate Surefire Report') {
            steps {
                sh 'mvn surefire-report:report'
            }
        }
        stage('pmd') {
          steps {
             sh 'mvn pmd:pmd'
          }
        }
      }

       post {
             always {
                   archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
                   archiveArtifacts artifacts: '**/target/*-javadoc.jar', fingerprint: true
                   archiveArtifacts artifacts: '**/target/surefire-reports/*.xml', fingerprint: true
                   archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
                   archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
            }
       }
}