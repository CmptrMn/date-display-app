def label = "worker-${UUID.randomUUID().toString()}"

podTemplate(label: label,
containers: [
    containerTemplate(name: 'node', image: 'node:carbon-jessie', command: 'cat', ttyEnabled: true),
    containerTemplate(name: 'docker', image: 'docker', command: 'cat', ttyEnabled: true),
    containerTemplate(name: 'kubectl', image: 'lachlanevenson/k8s-kubectl:v1.8.8', command: 'cat', ttyEnabled: true)
],
volumes: [
    hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock')
]) {
    node(label) {
        stage('Checkout repo') {
            checkout scm
        }

        stage('Run tests') {
            container('node') {
                sh('npm install')
                sh('npm test')
            }
        }
    }
}