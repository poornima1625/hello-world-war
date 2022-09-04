pipeline {
    agent any

    stages {
        stage('Checkout src') {
            steps {
                echo 'Java-Maven-war-project '
                echo "Branch_Name: ${env.GIT_BRANCH}" 
                //echo "${env.BRANCH_NAME}"
                //echo "${env.GIT_BRANCH}"//This will give me the Branch name
                git 'https://github.com/rranjith406/hello-world-war.git'
                sh 'ls -lrt'
                dir('dist') {
              		//sh 'mvn clean install -DskipTests'
              		echo 'cd to dist folder'
              		sh 'ls -lrt'
                }
            }
        }
        stage('Build Stage') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Test Stage') {
            steps {
                sh 'mvn clean test'
            }
        }
        stage('Deploy Stage') {
            steps {
                echo 'This is Deploy stage (TBD)'
                sh 'echo Build ${BUILD_NUMBER}'
                sshagent(['tomcat-id']) {
                    sh 'scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/Java_src_PipelineJob/target/hello-world-war-1.0.0.war ubuntu@172.31.32.178:/opt/tomcat/webapps' 
                }
            }
        }
    }
}
