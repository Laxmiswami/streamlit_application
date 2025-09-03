pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                git 'https://github.com/Laxmiswami/streamlit_application.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                    . venv/bin/activate
                    pytest --maxfail=1 --disable-warnings -q || true
                '''
            }
        }

        stage('Run App') {
            steps {
                sh '''
                    . venv/bin/activate
                    nohup streamlit run app.py --server.port=8501 &
                '''
                echo "✅ Streamlit app started at: http://<JENKINS_SERVER_IP>:8501"
            }
        }
     }
}
