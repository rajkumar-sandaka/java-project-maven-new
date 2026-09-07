pipeline {

    agent any

    stages {

        stage('Clean Workspace') {
            steps {
                deleteDir()
            }
        }

        stage('Checkout Developer Repository') {
            steps {
                dir('java-project-maven-new') {
                    git(
                        branch: 'master',
                        url: 'https://github.com/rajkumar-sandaka/java-project-maven-new.git'
                    )
                }
            }
        }

        stage('Checkout JMeter Repository') {
            steps {
                dir('ICP') {
                    git(
                        branch: 'main',
                        url: 'https://github.com/RajkumarSandaka/ICP.git'
                    )
                }
            }
        }

        stage('Run JMeter') {
            steps {
                dir('ICP') {
                    bat '''
                        if not exist results mkdir results

                        "C:\\apache-jmeter-5.6.3\\bin\\jmeter.bat" ^
                            -n ^
                            -t "Ship_Registration_21_08_2026.jmx" ^
                            -l "results\\result.jtl" ^
                            -e ^
                            -o "results\\html-report"
                    '''
                }
            }
        }
    }

    post {
        always {
            archiveArtifacts(
                artifacts: 'ICP/results/**/*',
                allowEmptyArchive: true
            )
        }
    }
}
