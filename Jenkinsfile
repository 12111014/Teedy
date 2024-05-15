// pipeline {
//       agent any
//       stages {
//         stage('Build') {
//           steps {
//              sh 'mvn -B -DskipTests clean package'
//           }
//          }
//
//         stage('Generate Javadoc') {
//             steps {
//                 sh 'mvn javadoc:jar'
//             }
//         }
//
//       stage('Generate Surefire Report') {
//             steps {
//                 sh 'mvn surefire-report:report'
//             }
//         }
//         stage('pmd') {
//           steps {
//              sh 'mvn pmd:pmd'
//           }
//         }
//       }
//
//        post {
//              always {
//                    archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
//                    archiveArtifacts artifacts: '**/target/*-javadoc.jar', fingerprint: true
//                    archiveArtifacts artifacts: '**/target/surefire-reports/*.xml', fingerprint: true
//                    archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
//                    archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
//             }
//        }
// }
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Building image') {
             steps{
                sh 'docker build -t teedy2024_manual .'
            }
        }
        stage('Upload image') {
            steps{
            //your command
                //sh 'docker tag teedy2024_manual jimmy889/teedy_local:latest'
                sh 'docker push jimmy889/teedy_local:latest'
            }
        }
        stage('K8s') {
            steps {
                sh 'kubectl set image deployments/hello-node docs=jimmy889/teedy_local:latest'
            }
        }
    }
}