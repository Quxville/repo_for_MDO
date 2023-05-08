pipeline {
    parameters {
        string(name: 'VERSION', defaultValue: '0.0.0', description: '')
        booleanParam(name: 'PROMOTE', defaultValue: true, description: '')
    }
    agent any
    stage('Clone') {
    steps {
        sh 'docker volume prune -f'
        sh 'docker volume create volin'
        sh 'docker run -v volin:/data --name buffer ubuntu'
        sh 'docker cp ~/.ssh/id_rsa buffer:/root/.ssh/id_rsa'
        sh 'docker cp ~/.ssh/id_rsa.pub buffer:/root/.ssh/id_rsa.pub'
        sh 'docker exec buffer sh -c "chmod 600 /root/.ssh/id_rsa && chmod 644 /root/.ssh/id_rsa.pub"'
        sh 'docker exec buffer sh -c "ssh-keyscan -t rsa github.com > /root/.ssh/known_hosts"'
        sh 'docker exec buffer sh -c "git clone https://github.com/irssi/irssi.git /data/irssi"'
        sh 'docker rm buffer'
        echo 'Cloning...'
    }
}

}
