pipeline {
  agent {
    docker {
      image 'maven:3.6.3-jdk-11-slim'
    }

  }
  stages {
    stage('build') {
      when {
		beforeAgent true
		branch 'master' 
	 }
      steps {
        echo 'compiling sysfoo app'
        sh 'mvn compile'
      }
    }

    stage('test') {
	when {
		beforeAgent true
		branch 'master' 
	 }

      steps {
        echo 'test sysfoo app'
        sh 'mvn clean test'
      }
    }

    stage('package') {
	when {
		beforeAgent true
		branch 'master' 
	 }
      steps {
        echo 'packaging sysfoo app'
        sh 'mvn package -DskipTests'
        archiveArtifacts 'target/*.war'
      }
    }

  }
  stage('Deploy to Dev') {
      when {
             beforeAgent true
             branch  'master'
       }

      agent any

      steps {
        echo 'Deploying to Dev Environment with Docker Compose'
        sh 'docker-compose up -d'
      }
    }	
  tools {
    maven 'Maven 3.6.3'
  }
}
