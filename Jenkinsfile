node() {
    stage('Build with Gradle') {
        sh "./gradlew"
    }
    stage('Create Jobs') {
        pipelineDsl targets: [ 'jobs/Jenkinsfile', 'views/*.groovy' ].join('\n'),
               additionalClasspath: ['src/**/*.groovy', 'src/**/*.jar',
                                     'lib/**/*.groovy', 'lib/**/*.jar'].join('\n'),
              removedJobAction: 'DELETE',
              removedViewAction: 'DELETE',
              failOnMissingPlugin: true,
              unstableOnDeprecation: true
    }
}
