pipeline {
    agent any
	environment{
		PYTEST = '/f/python/Jenkins/env36/Scripts/py.test'
		PYINSTALLER = '/f/python/Jenkins/env36/Scripts/pyinstaller'
	}
    stages {
        stage('Build') {
            steps {
                sh 'python -m py_compile sources/add2vals.py sources/calc.py'
            }
        }
        stage('Test') {
            steps {
                sh '$PYTEST --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
            }
            post {
                always {
                    junit 'test-reports/results.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh '$PYINSTALLER --onefile sources/add2vals.py'
            }
            post {
                success {
                    archiveArtifacts 'dist/add2vals.exe'
                }
            }
        }
    }
}

