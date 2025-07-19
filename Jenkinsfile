node {
    
    def mavenHome=tool name: "Maven3.9.9"

    stage('Checkout') {
        git branch: 'development',
            credentialsId: 'e7967c99-09e4-405a-9e72-a39e1b637692',
            url: 'https://github.com/khasimlearn/maven-web-app-project-kk-funda.git'
    }

    stage('Build') {
        sh "${mavenHome}/bin/mvn clean package"
    }

    stage('SonarQube Report') {
        sh "${mavenHome}/bin/mvn clean package sonar:sonar"
    }

    stage('Nexus') {
        sh "${mavenHome}/bin/mvn deploy"
    }
    stage('Deploy to Tomcat') 
    {
        echo "Deploying WAR file using curl..."

        sh """
            curl -u khasim:khasim \
            --upload-file /var/lib/jenkins/workspace/JioScripted//target/maven-web-application.war \
            "http://65.0.105.56:8080/manager/text/deploy?path=/maven-web-application&update=true"
        """
    }
}
