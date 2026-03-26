node {
    def appDir = '/var/www/nextjs-app'

    stage('CLean Workspace'){
        echo 'Cleaning Jenkins Worksapce'
        deleteDir()
    }

    stage('clone repo'){
        echo 'clonning the repo'
        git(
            branch : 'main',
            url : 'https://github.com/Teja-swaroop141/ci-cd--jenkins-AWS.git'
        )
    }

    stage('Deploy to Ec2'){
        echo 'Deploying to ec2 instance'
        sh """ 
            sudo mkdir -p ${appDir}
            sudo chown -R jenkins:jenkins ${appDir}

            rsync -av --delete --exclude='.git' --exclude='node_modules' ./ ${appDir}

            cd ${appDir}
            sudo npm install 
            sudo npm run build 
            sudo fuser -k 3000/tcp || true 
            npm run start 

        """
    }

}