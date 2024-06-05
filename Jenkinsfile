pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Akhilendra-K-Thakur/CalendarApp.git', branch: 'master'
            }
        }
        stage('Build') {
            steps {
                sh 'xcodebuild -workspace MyApp.xcworkspace -scheme MyAppScheme -sdk iphonesimulator -destination "platform=iOS Simulator,name=iPhone 11,OS=14.4" clean build'
            }
        }
        stage('Test') {
            steps {
                sh 'xcodebuild test -workspace MyApp.xcworkspace -scheme MyAppScheme -sdk iphonesimulator -destination "platform=iOS Simulator,name=iPhone 11,OS=14.4" | xcpretty'
            }
        }
        stage('Archive') {
            steps {
                sh 'xcodebuild -workspace MyApp.xcworkspace -scheme MyAppScheme -sdk iphoneos -archivePath $PWD/build/MyApp.xcarchive archive'
            }
        }
        stage('Export') {
            steps {
                sh 'xcodebuild -exportArchive -archivePath $PWD/build/MyApp.xcarchive -exportOptionsPlist ExportOptions.plist -exportPath $PWD/build'
            }
        }
    }
    post {
        always {
            // Clean up actions, such as archiving build artifacts or sending notifications
            archiveArtifacts artifacts: 'build/**/*.ipa', allowEmptyArchive: true
        }
    }
}
