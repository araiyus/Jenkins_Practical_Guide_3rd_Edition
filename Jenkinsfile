pipeline {
    agent any
    tools {
        maven "Maven 3.5.0"
        jdk "JDK8"
    }
    stages {
        stage('チェックアウト') {
            steps {
                // Gitリポジトリの指定
                git url: 'https://github.com/araiyus/Jenkins_Practical_Guide_3rd_Edition.git'
            }
        }
        stage('Mavenビルド') {
            steps {
                bat "mvn clean package"
            }
        }
        stage('テスト結果の集計') {
            steps {
                // JUnitテスト結果の集計
                junit('target/surefire-reports/*.xml')
                // JaCoCo結果の集計
                // jacoco(execPattern: 'target/jacoco.exec')
                }
            }
        stage('コード解析結果の集計') {
            steps {
                // Checkstyle結果の集計
                checkstyle(pattern: 'target/checkstyle-result.xml')
                // FindBugs結果の集計
                findbugs(pattern:'target/findbugsXml.xml')
            }
        }
    }
}