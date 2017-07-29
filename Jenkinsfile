pipeline {
    agent any

    stages {
        stage('setup') {
          steps {
                echo 'Setting up environment'
                sh  sudo -y install wget unzip
	        sh  '''if [[ ! -f /usr/local/bin/packer ]]; then
                        wget https://releases.hashicorp.com/packer/1.0.3/packer_1.0.3_linux_amd64.zip
                        cd /usr/local/bin
                        unzip packer_1.0.3_linux_amd64.zip
                   fi'''
          }
        }
        stage('Unit') {
            steps {
                echo 'Unit Testing..'
                sh /usr/local/bin/packer validate centos/centos7.json
                sh /usr/local/bin/packer inspect centos/centos7.json

            }
        }
        stage('Build') {
            steps {
                echo 'Building Centos7..'
                sh /usr/local/bin/packer build centos/centos7.json
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying Image'
                sh cp  output-virtualbox-iso/centos7-base-0.1.0-disk001.vmdk /vms/images/centos/centos7/
            }
        }
    }
}

