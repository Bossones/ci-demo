pipeline {
  agent any
  stages {
    // Мы используем тут master агента, что очень плохо в реальных проектах
    // Для демо целей - это позволительно, поэтому надо сюда установить python
    stage('Preparation') {
      steps {
        sh """
          whoami
          ls -la
          apt install -y python3 python3-pip
          ln -s /usr/bin/python3 /usr/bin/python
        """
      }
    }
    stage('Build and Test') {
      steps {
        sh """
          pip install -r requirements.txt
          ls -la
          python hello-world.py
          echo "The code is okay"
        """
      }
    }
    stage('Lint') {
      steps {
        sh """
          pip install -r requirements.txt
          flake8 . --extend-exclude=dist,build --show-source --statistics
        """
      }
    }
  }
}
