pipeline {
    environment {
        // Define any environment variables here
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Akhilendra-K-Thakur/CalendarApp.git', branch: 'master'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'bundle install' // If you are using Bundler for dependency management
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
        failure {
            // Actions to take in case of failure, such as sending notifications
        }
        success {
            // Actions to take on successful build, such as deploying or further processing
        }
    }
}
