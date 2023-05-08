pipeline {
    parameters {
        string(name: 'VERSION', defaultValue: '0.0.0', description: '')
        booleanParam(name: 'PROMOTE', defaultValue: true, description: '')
    agent any

    stages {
        stage('Clone') {
            steps {
                sh 'docker volume prune -f'
                sh 'docker volume create volin'
                sh 'docker run -v volin:/data --name buffer ubuntu'
                sh 'docker cp /dev/null buffer:/data/known_hosts'
                sh 'docker run --rm --name git-ssh -v /path/to/ssh:/root/.ssh -w /root/.ssh ubuntu sh -c "apt-get update && apt-get install -y git && chmod 400 id_rsa && ssh-keyscan github.com >> known_hosts"'
                sh 'docker run --rm --name git -v volin:/app --volumes-from git-ssh ubuntu sh -c "git clone https://github.com/irssi/irssi.git /app/irssi"'
                sh 'docker rm buffer git-ssh git'
                echo 'Cloning...'
            }
        }
    }
}

