pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url:'https://github.com/Leetfs/test-jenkins-c'
            }
        }
        stage('Cross-compile') {
            steps {
                sh '''
                    x86_64-w64-mingw32-gcc -o hello.exe hello.c

                    if [ -f hello.exe ]; then
                        echo "Compilation successful"
                    else
                        echo "Compilation failed"
                        exit 1
                    fi
                '''
            }
        }
        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'hello.exe', onlyIfSuccessful: true
            }
        }
    }
}
