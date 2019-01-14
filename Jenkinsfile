pipeline {
  agent {
    kubernetes {
      label 'taaspod'
      defaultContainer 'jnlp'
      yaml """
apiVersion: v1
kind: Pod
metadata:
  labels:
    app: taas-jenkins-slave
spec:
  containers:
  - name: taas
    image: zyb2n/taastest:1.5
    command:
    - cat
    tty: true
"""
    }
  }


  stages {
    stage('build') {
      steps {
        container('taas') {
          sshagent (credentials: ['taas-ssh']) {
	    sh 'git clone https://github.com/zyb2n/taas-pipeline-04.git /tmp/taas-pipeline-04'
// load saved objects to kibana
	    sh 'cd /tmp/taas-pipeline-04/kibana/saved && ./import.sh'
         }
        }
      }

    }

}
  }

}
