pipeline {
  agent any
  tools {
    jdk 'Java'
  }

  environment {
    JAVA_HOME = tool 'Java'
    PATH = "${env.JAVA_HOME}\\bin;${env.PATH}"
  }

  stages {
    stage('Checkout') {
      steps {
        git url: 'https://github.com/por314159ug/app-java.git', branch: 'main'
      }
    }

    stage('Compile') {
      steps {
        bat '''
          if not exist build\\classes mkdir build\\classes
          javac -d build\\classes Main.java
        '''
      }
    }

    stage('Prepare Manifest') {
      steps {
        bat '''
          if not exist build\\classes mkdir build\\classes
          echo Main-Class: Main > build\\classes\\manifest.txt
        '''
      }
    }

    stage('Package') {
      steps {
        bat '''
          if not exist build\\jar mkdir build\\jar
          jar cfm build\\jar\\MyApplication.jar build\\classes\\manifest.txt -C build\\classes .
        '''
      }
    }

    stage('Run') {
      steps {
        bat '''
          java -jar build\\jar\\MyApplication.jar
        '''
      }
    }
  }
}
