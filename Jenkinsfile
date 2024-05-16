pipeline {
    agent any

    stages {
        stage('Cleanup Workspace') {
            steps {
                cleanWs()
            }
        }
        
        stage('Checkout') {
            steps {
                git url: 'https://github.com/lololis/VulnerableJavaWebApplication.git'
            }
        }
        
        stage('Fortify Remote Arguments') {
        steps {
            fortifyRemoteArguments transOptions: '-Xmx4G',
            scanOptions: '"-analyzers" "controlflow,dataflow"'
            }
        }
        stage('Fortify Remote Analysis') {
        steps {
                fortifyRemoteAnalysis remoteAnalysisProjectType: fortifyPHP(),
                uploadSSC: [appName: 'SAST_25', appVersion: 'v25']
                }
            }
        stage('Build') {
            steps {
                echo "Complete!"
            }
        }
    }
}
