node {
    // Mark the code checkout 'stage'....
    stage 'Checkout'
    // Get some code from a GitHub repository
    git credentialsId: 'cb29c585-5f90-4907-98f2-1a81cfe9fb2d', url: 'https://gitlab.com/yonezawahr/Jenkins_Practical_Guide_2nd_Edition.git'

    // Get the maven tool.
    // Global Tool Configuration Ç≈ Maven 3.3.9 Çê›íËÇµÇƒÇ¢ÇÈÇ±Ç∆ÅB
    def mvnHome = tool 'Maven 3.3.9'

    // Mark the code build 'stage'....
    stage 'Build, Unittest and Coverage'
    // Run the maven build
    if (env.OS == "Windows_NT") {
        bat "${mvnHome}/bin/mvn clean package"
    } else {
        sh "${mvnHome}/bin/mvn clean package"
    }

    // Mark the Report of Unittest and Coverage 'stage'....
    stage 'Report of Unittest and Coverage'
    junit '**/target/surefire-reports/TEST-*.xml'
    step([$class: 'JacocoPublisher'])

    // Mark the Static Analysis 'stage'....
    stage 'Static Analysis'
    step([$class: 'CheckStylePublisher', canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '**/target/checkstyle-result.xml', unHealthy: ''])
    step([$class: 'FindBugsPublisher', canComputeNew: false, defaultEncoding: '', excludePattern: '', healthy: '', includePattern: '', pattern: '**/target/findbugsXml.xml', unHealthy: ''])
}
