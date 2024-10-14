pipeline {

    agent any
    tools{
        maven 'maven'
    }

    stages{

        stage('version increment'){
            steps{
                script{
                    echo " incrementing application version......."
                    sh 'mvn build-helper:parse-version versions:set \
                       -DnewVersion=\\\${parsedVersion.majorVersion}.\\\${parsedVersion.minorVersion}.\\\${parsedVersion.nextIncrementalVersion} \
                       versions:commit'
                    def matcher = readFile('pom.xml') =~ '<version>(.+)</version>'
                    def version = matcher[0][1]
                    env.IMAGE_NAME = "$version-$BUILD_NUMBER"
                }
            }
        }

        stage('build jar'){
            steps{
                script{
                    echo 'packaging application into jar file .....'
                    sh 'mvn clean package'
                }
            }
        }

        stage('build image'){
            steps{
                script{
                    echo ' building application into docker image.....'
                    sh "docker build -t nanaot/java-app:$IMAGE_NAME ."
                }
            }
        }
        stage('push image'){
            steps{
                script{
                    echo 'pushing docker image into private registry......'
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'USER', passwordVariable: 'PASS')]){
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh "docker push nanaot/java-app:$IMAGE_NAME"
                    }
                }
            }
        }

        stage('deploy application'){
            steps{
                script{
                    echo 'deploying application'
                }
            }
        }

        stage('commit changes'){
            steps{
                script{
                    echo 'commiting changes into git registry.....'
                    withCredentials([usernamePassword(credentialsId:'github-credentials', usernameVariable: 'USER', passwordVariable: 'PASS')]){

                        sh 'git config --global user.email "jenkins@example.com"'
                        sh 'git config --global user.name "jenkins"'
                        sh "git remote set-url origin https://${USER}:${PASS}@github.com/bondgh0954/Jenkins-final.git"
                        sh 'git add .'
                        sh 'git commit -m "commiting changes"'
                        sh 'git push origin HEAD:main'
                    }
                }    
            }
        }


    }
}