pipeline {
    agent any

    stages {
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
