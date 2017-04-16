pipeline {
    agent any
    tools {
        maven "Maven 3.5.0"
        jdk "JDK8"
    }
    stages {
        stage('Maven�r���h') {
            steps {
                bat "mvn clean package"
            }
        }
        stage('�e�X�g���ʂ̏W�v') {
            steps {
                // JUnit�e�X�g���ʂ̏W�v
                junit('target/surefire-reports/*.xml')
                // JaCoCo���ʂ̏W�v
                // jacoco(execPattern: 'target/jacoco.exec')
                }
            }
        stage('�R�[�h��͌��ʂ̏W�v') {
            steps {
                // Checkstyle���ʂ̏W�v
                checkstyle(pattern: 'target/checkstyle-result.xml')
                // FindBugs���ʂ̏W�v
                findbugs(pattern:'target/findbugsXml.xml')
            }
        }
    }
}