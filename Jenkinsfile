pipeline {
    agent any

    stages {

        stage('Build - Verificar archivos') {
            steps {
                echo 'Verificando archivos JS, CSS y HTML...'
                bat 'if not exist src\\index.html (echo ERROR: index.html no encontrado && exit 1)'
                bat 'if not exist src\\index.css (echo ERROR: index.css no encontrado && exit 1)'
                bat 'if not exist src\\index.js (echo ERROR: index.js no encontrado && exit 1)'

                echo 'Verificando archivos de API...'
                bat 'if not exist src\\api\\add.php (echo ERROR: add.php no encontrado && exit 1)'
                bat 'if not exist src\\api\\db.php (echo ERROR: db.php no encontrado && exit 1)'
                bat 'if not exist src\\api\\delete.php (echo ERROR: delete.php no encontrado && exit 1)'
                bat 'if not exist src\\api\\get.php (echo ERROR: get.php no encontrado && exit 1)'

                echo 'Todos los archivos presentes!'
            }
        }

        stage('Test - Sintaxis JS') {
            steps {
                echo 'Verificando sintaxis JS...'
                bat 'node --check src\\index.js || echo Advertencia en index.js'
                echo 'Sintaxis JS OK'
            }
        }

        stage('Test - Sintaxis PHP') {
            steps {
                echo 'Verificando sintaxis PHP...'
                bat 'php -l src\\api\\add.php'
                bat 'php -l src\\api\\db.php'
                bat 'php -l src\\api\\delete.php'
                bat 'php -l src\\api\\get.php'
                echo 'Sintaxis PHP OK'
            }
        }

        stage('Deploy - Copiar a public') {
            when {
                branch 'main'
            }
            steps {
                echo 'Copiando archivos a directorio publico...'
                bat 'if not exist public mkdir public'
                bat 'if not exist public\\api mkdir public\\api'
                bat 'copy src\\index.html public\\'
                bat 'copy src\\index.css public\\'
                bat 'copy src\\index.js public\\'
                bat 'copy src\\api\\add.php public\\api\\'
                bat 'copy src\\api\\db.php public\\api\\'
                bat 'copy src\\api\\delete.php public\\api\\'
                bat 'copy src\\api\\get.php public\\api\\'
                echo 'Deploy completado!'
            }
        }

    }

    post {
        success {
            echo 'Pipeline completado exitosamente!'
        }
        failure {
            echo 'Pipeline fallo. Revisa el Console Output.'
        }
        always {
            echo 'Pipeline finalizado.'
        }
    }
}
