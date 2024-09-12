pipeline {
  agent none
  stages {
    // Мы используем тут master агента, что очень плохо в реальных проектах
    // Для демо целей - это позволительно, поэтому надо сюда установить python
    stage('Build and Test') {
      agent {         
       docker {          
         image 'python:3.9.20-alpine3.20'         
       }    
      }
      steps {
        sh """
          pip install -r requirements.txt --user
          ls -la
          python hello-world.py
          echo "The code is okay"
        """
      }
    }
    stage('Lint') {
      agent {         
         docker {          
           image 'python:3.9.20-alpine3.20'         
        }    
      }
      steps {
        sh """
          pip install -r requirements.txt
          flake8 . --extend-exclude=dist,build --show-source --statistics
        """
      }
    }
  }
}
