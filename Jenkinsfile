pipeline {
    agent none
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'python:2-alpine'
                }
            }
            steps {
                sh 'python -m py_compile sources/add2vals.py sources/calc.py'
            }
        }
        stage('Test') {
            agent {
                docker {
                    image 'qnib/pytest'
                }
            }
            steps {
                sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
            }
            
            //post {
            //    always {
            //        junit 'test-reports/results.xml'
            //    }
            //}
            post {
                success {
                    sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
                }     
 //               always {
 //                   publishHTML target: [
 //                       allowMissing: false,
 //                       alwaysLinkToLastBuild: false,
 //                       keepAll: true,
 //                       reportDir: 'build/reports/tests/test',
 //                       reportFiles: 'index.html',
 //                       reportName: 'Junit Report'
 //                   ]
 //                   publishHTML target: [
 //                       allowMissing: false,
 //                       alwaysLinkToLastBuild: false,
 //                       keepAll: true,
 //                       reportDir: 'build/reports/jacoco/test/html',
 //                       reportFiles: 'index.html',
 //                       reportName: 'Code Coverage Report'
 //                   ]
 //               }
            }
        }
        //stage('Deliver') { 
        //    agent {
        //        docker {
        //            image 'cdrx/pyinstaller-linux:python2' 
        //        }
        //    }
        //    steps {
        //        sh 'pyinstaller --onefile sources/add2vals.py' 
        //    }
        //    post {
        //        success {
        //            archiveArtifacts 'dist/add2vals' 
        //        }
        //    }
        //}
    }
}
