pipeline {
    agent any
    
    // {
       
        // docker {
        //     image 'maven:3-alpine'
        //     args '-v /root/.m2:/root/.m2'
        // }
    // }
    options {
        skipStagesAfterUnstable()
    }
    stages 
    {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Publish to Nexus') {
            steps {
                nexusPublisher nexusInstanceId: 'nexus-repo', nexusRepositoryId: 'maven-release', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: 'jar', filePath: './target/my-app-1.0-SNAPSHOT.jar']], mavenCoordinate: [artifactId: 'my-app-1.0-SNAPSHOT.jar', groupId: 'com.mycompany.app', packaging: 'jar', version: '1.0']]], tagName: '1.1.1'                 
                
            }
        }
    }
}
