podTemplate(
    label: 'abc', 
    inheritFrom: 'default',
    containers: [
        containerTemplate(
            name: 'docker', 
            image: 'docker:18.02',
            ttyEnabled: true,
            command: 'cat'
        ),
        containerTemplate(
            name: 'helm', 
            image: 'ibmcom/k8s-helm:v2.6.0',
            ttyEnabled: true,
            command: 'cat'
        ), containerTemplate(
               name: 'kubectl', 
               image: 'lachlanevenson/k8s-kubectl:v1.6.6', 
               ttyEnabled: true, 
               command: 'cat'
        )
    ], 
    volumes: [
        hostPathVolume(
            hostPath: '/var/run/docker.sock',
            mountPath: '/var/run/docker.sock'
        )
    ]
) {
    node('abc') {
        def commitId
        stage ('Extract') {
            checkout scm
            commitId = sh(script: 'git rev-parse --short HEAD', returnStdout: true).trim()
        }
        stage ('Deploy') {
            container ('helm') {
                //sh "helm init --upgrade --client-only --skip-refresh"
                sh "helm ls"
                sh "helm upgrade --install my-grafana grafana"
                sh "helm ls"
            }
        }
    }
}
