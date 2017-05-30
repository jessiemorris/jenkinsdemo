def projectName = currentBuild.fullProjectName.split('/')[0].replaceFirst('_', '/')

node() {
    checkoutStage {
        deleteDir()
        label = "Checkout"
        project = projectName
    }
    stage('Build with Gradle') {
        sh "./gradlew"
    }
    stage('Create Jobs') {
        jobDsl targets: [ 'jobs/*.groovy', 'views/*.groovy' ].join('\n'),
               additionalClasspath: ['src/**/*.groovy', 'src/**/*.jar',
                                     'lib/**/*.groovy', 'lib/**/*.jar'].join('\n'),
              removedJobAction: 'DELETE',
              removedViewAction: 'DELETE',
              failOnMissingPlugin: true,
              unstableOnDeprecation: true
    }
}
