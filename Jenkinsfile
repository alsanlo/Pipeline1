pipeline {
  agent any
  stages {
    stage('Inicializacion') {
      steps {
        echo 'Inicializando.....'
        sh 'date'
      }
    }
    stage('Build') {
      steps {
        writeFile(file: 'File1', text: 'Esta es la construcción de un nuevo archivo desde el pipeline')
        build 'JobCreartedByBOc'
      }
    }
    stage('Test') {
      parallel {
        stage('Test') {
          steps {
            fileExists 'File1'
            catchError() {
              archiveArtifacts(allowEmptyArchive: true, caseSensitive: true, defaultExcludes: true, artifacts: 'art1')
            }

          }
        }
        stage('Paralelo 1') {
          steps {
            echo 'Esto es la muestra de un código en paralelo'
          }
        }
        stage('Paralelo2') {
          steps {
            echo 'Esto es la muestra de un código en paralelo'
          }
        }
      }
    }
    stage('Deploy') {
      steps {
        ws(dir: 'Pipeline2')
      }
    }
    stage('End of this Pipeline') {
      steps {
        sleep(unit: 'SECONDS', time: 20)
      }
    }
  }
}