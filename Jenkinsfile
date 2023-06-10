def clone(branch,url,credential){
checkout([
        $class: 'GitSCM', 
        branches: [[name: branch]], 
        doGenerateSubmoduleConfigurations: false, 
        extensions: [[$class: 'CleanCheckout']], 
        submoduleCfg: [], 
        userRemoteConfigs: [[credentialsId: credential, url: url]]
    ])

}


pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Mengambil kode dari repository
                clone("stagging","https://github.com/Mdzikri/tubes-cilsy.git","github_cred")
            }
        }
        
        stage('Build image') {
            steps {
                // Menjalankan proses build
                sh "docker build -t ${params.name}:${params.version}"
            }
        }
        
        // stage('Test') {
        //     steps {
        //         // Menjalankan proses pengujian
        //         sh ''
        //     }
        // }
        
        stage('Deploy') {
            steps {
                // Melakukan deployment ke server atau platform yang ditentukan
                sh "docker-compose up"
            }
        }
    }
}
