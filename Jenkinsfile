pipeline {
   agent {
       docker {
           image 'python:3.7.7-stretch'
           args '--network=skynet'
       }
   }

   stages {
      stage('Build') {
         steps {
            echo 'Baixando as depedências do projeto'
            sh 'pip install -r requirements.txt'
         }
      }
      stage('Test') {
         steps {
            echo 'Executando testes de regressão'
            sh 'robot -d ./logs tests/'
         }
         post {
            always {
               robot 'logs'
            }
         }
      }
      stage('UAT') {
         steps {
            echo 'Aprovação dos testes de aceitação' 
            input (message: 'Você aprova essa versão?', ok: 'Sim')
         } 
      }
      stage('Production') {
         steps {
            echo 'API Ok em produção!'
         } 
      }
   }
}
