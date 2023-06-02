pipeline {
    agent  any;
    stages {
        stage('Preparación entorno') {
	    agent {
		node {
		    label "principal";
      		}
   	    }
            steps {
                sh 'python3 -m pip install -r requirements.txt'
                sh 'echo "nombre de host $HOSTNAME y el usuario $USER"'
            }
        }
        stage('Control de calidad') {
	    agent {
		node {
		    label "principal";
      		}
   	    }
            steps {
                sh 'python3 -m pylint app.py'
                sh 'echo "nombre de host $HOSTNAME y el usuario $USER"'
            }
        }
        stage('Tests') {
	    agent {
		node {
		    label "principal";
      		}
   	    }
            steps {
                sh 'python3 -m pytest'
                sh 'echo "nombre de host $HOSTNAME y el usuario $USER"'
            }
        }
        stage('Build') {
	    agent {
		node {
		    label "DockerServer";
      		}
   	    }
            steps {
                sh 'docker build https://github.com/AlissonMMenezes/Chapter10.git -t chapter10:latest'
                sh 'echo "nombre de host $HOSTNAME y el usuario $USER"'
            }
        }        
        stage('Deploy') {
	    agent {
		node {
		    label "DockerServer";
      		}
   	    }
            steps {
                sh 'docker run -tdi -p 5000:5000 chapter10:latest'
                sh 'echo "nombre de host $HOSTNAME y el usuario $USER"'
            }
        }
    }
}
