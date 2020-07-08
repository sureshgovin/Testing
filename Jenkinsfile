pipeline {
agent any
// Run on a build agent where we have the Android SDK installed

stages {
stage('Compile') {
steps {
// Compile the app and its dependencies
sh './gradlew compileDebugSources'
}
}
stage('Unit test') {
steps {
// Compile and run the unit tests for the app and its dependencies
sh './gradlew testDebugUnitTest testDebugUnitTest'

 // Analyse the test results and update the build result as appropriate
  junit allowEmptyResults: true, testResults: '**/test-results/*.xml'

}
}
stage('Build APK') {
steps {
// Finish building and packaging the APK
sh './gradlew assembleDebug'

// Archive the APKs so that they can be downloaded from Jenkins
archiveArtifacts '**/*.apk'
}
}
stage('Deploy') {
steps {
// Build the app in release mode, and sign the APK using the environment variables
sh './gradlew assembleRelease'

// Archive the APKs so that they can be downloaded from Jenkins
archiveArtifacts '**/*.apk'

}

}

}
}