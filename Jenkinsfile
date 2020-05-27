pipeline {
    agent any
    tools {
        maven "Maven 3.6.3"
//        jdk "JDK8"
    }
    stages {
        stage('Hello World') {
            steps {
                library 'my-shared-library'
                helloWorld 'Yusuke'
            }
        }
        stage('チェックアウト') {
            steps {
                git url: 'https://github.com/yusuke-imt/Jenkins_Practical_Guide_3rd_Edition.git'
            }
        }
       stage('Maven build') {
            steps {
                sh "mvn clean package"
            }
        }
                stage('test results aggregate') {
            steps {
                junit('target/surefire-reports/*.xml')
                step([$class: 'JacocoPublisher', execPattern: 'target/jacoco.exec'])
            }
        }
        stage('code analyse results aggregate') {
            steps {
                checkstyle(pattern: 'target/checkstyle-result.xml')
                findbugs(pattern:'target/findbugsXml.xml')
            }
        }
        stage('sample job call') {
            steps {
                build job: 'SampleJob', parameters: [string(name:'MESSAGE', value: params.PERSON)]
            }
        }
    }
}
