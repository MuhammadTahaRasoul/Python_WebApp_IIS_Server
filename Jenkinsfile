pipeline {

    agent any

    environment {

        APP_DIR = 'C:\\Users\\Taha\\Desktop\\Study Material\\Dream\\Demo Project\\Python_Web_App'
        VENV = 'C:\\Users\\Taha\\Desktop\\Study Material\\Dream\\Demo Project\\Python_Web_App\\venv'
        SERVICE = 'FlaskWebApp'

    }

    stages {

        stage('Checkout') {

            steps {
                checkout scm
            }

        }

        stage('Install Dependencies') {

            steps {

                bat '''
                    if not exist "%VENV%" (
                        python -m venv "%VENV%"
                    )

                    "C:\\Users\\Taha\\AppData\\Local\\Programs\\Python\\Python311\\python.exe" -m pip install -r requirements.txt
                '''

            }

        }

        stage('Test') {

            steps {

                bat '''
                    "%VENV%\\Scripts\\python.exe" -m py_compile app.py
                '''

            }

        }

        stage('Deploy') {

            steps {

                bat '''
                    xcopy /E /Y /I "%WORKSPACE%\\app.py" "%APP_DIR%\\"
                    xcopy /E /Y /I "%WORKSPACE%\\templates" "%APP_DIR%\\templates\\"
                    copy /Y "%WORKSPACE%\\requirements.txt" "%APP_DIR%\\"
                '''

            }

        }

        stage('Restart Application') {

            steps {

                bat '''
                    net stop "%SERVICE%"
                    net start "%SERVICE%"
                '''

            }

        }

    }

    post {

        success {
            echo 'Deployment successful!'
        }

        failure {
            echo 'Deployment failed!'
        }

    }
}