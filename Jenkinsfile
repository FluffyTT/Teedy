pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Doc') {
            steps {
                sh 'mvn site --fail-never'
            }
        }
        stage('pmd') {
            steps {
                sh 'mvn pmd:pmd'
            }
        }
        stage('Test report') {
            steps {
                sh 'mvn mvn test --fail-never'
                sh 'mvn surefire-report:report'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: '**/target/site/pmd.html', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
            archiveArtifacts artifacts: '**/target/site/surefire-report.html', fingerprint: true
            archiveArtifacts artifacts: '**/target/site/apidocs', fingerprint: true
        }
    }
}
