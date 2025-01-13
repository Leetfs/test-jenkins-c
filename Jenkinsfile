pipeline {
    agent any
    stages {
        stage('Clean Workspace') {
            steps {
                script {
                    deleteDir()  // 清空当前工作区
                }
            }
        }
        stage('Checkout') {
            steps {
                git branch: 'main', url:'https://github.com/Leetfs/test-jenkins-c'
            }
        }
        stage('Cross-compile') {
            steps {
                sh '''
                    mkdir -p build
                    cd build
                    cmake -DCMAKE_TOOLCHAIN_FILE=../toolchain.cmake ../
                    make

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
                archiveArtifacts artifacts: 'build/hello.exe', onlyIfSuccessful: true
            }
        }
    }
}
