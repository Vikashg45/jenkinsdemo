node {
    def appDir = '/var/www/nextjs-app'

    stage('Clean Workspace'){
        echo 'Cleaning Jenkins Workspace'
        deleteDir()
    }

    stage('Clone Repo'){
        echo 'cloning the Repo'
        git(
            branch: 'main',
            url: 'https://github.com/Vikashg45/jenkinsdemo.git'
        )
    }

    stage('Deploy to Ec2'){
        echo 'Deploying to Ec2'
        sh """
            sudo mkdir -p ${appDir}
            sudo chown -R jenkins:jenkins ${appDir}

            rsync -av --delete \
            --exclude='.git' \
            --exclude='node_modules' \
            ./ ${appDir}

            cd ${appDir}
            sudo npm install
            sudo npm run build
            sudo fuser -k 3000/tcp || true
            npm run start
        """
    }
}
