pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'echo "Running on Linux"'
                    } else {
                        bat '''
                        set PATH=C:\\Windows\\System32;%PATH%
                        echo "Running on Windows"
                        '''
                    }
                }
            }
        }
    }
}
