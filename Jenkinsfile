pipeline {
    agent any

    stages {
        stage('setup') {
          steps {
                echo 'Setting up environment'
                sh  'sudo apt install wget unzip'
	        sh  '''if [[ ! -f /usr/local/bin/packer ]]; then
                        cd /usr/local/bin
                        sudo wget https://releases.hashicorp.com/packer/1.0.3/packer_1.0.3_linux_amd64.zip
                        sudo unzip packer_1.0.3_linux_amd64.zip
                   fi'''
          }
        }
        stage('Unit') {
            steps {
                echo 'Unit Testing..'
                sh '/usr/local/bin/packer validate centos7/centos.json'
                sh '/usr/local/bin/packer inspect centos7/centos.json'

            }
        }
        stage('Build') {
            steps {
                echo 'Building Centos7..'
                sh '/usr/local/bin/packer build -color=false centos7/centos.json'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying Image'
                sh 'cp  output-virtualbox-iso/centos7-base-0.1.0-disk001.vmdk /vms/images/centos/centos7/'
            }
        }
    }
}

