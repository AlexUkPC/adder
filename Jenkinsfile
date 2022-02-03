pipeline {
    agent {
        dockerfile {
            label 'ssh'
      }   
    }
    parameters {
        string(name: 'REF', defaultValue: '\${ghprbActualCommit}', description: 'Commit to build')
    }
    stages {
        stage('Compile') {
            steps {
                sh 'python3 -m compileall adder.py'
            }   
        }
        stage('Run') {
            steps {
                sh 'python3 adder.py 3 5'
            }   
        }
        stage('Unit test') {
            steps {
                sh '''python3 -m pytest \
                    -v --junitxml=junit.xml \
                    --cov-report xml --cov adder adder.py
                '''
            }   
        }   
        stage('Hello GitHub') {
            steps {
                echo "Hello GitHub!2"
            }   
        }
    }
    post {
        always {
            junit 'junit.xml'
            cobertura coberturaReportFile: 'coverage.xml'
        }
    }
}