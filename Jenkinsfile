node {
    stage('Git checkout') {
        git branch: "${params.BRANCH}", url: 'https://github.com/Projet-Automation-Infra-SI-Ynov/Images'
    }
    stage('Add user for login to registry') {
        sh "sed -i 's/USER/${params.USERNAME}/g' ./image.yml"
    }
    stage('Add password for login to registry') {
        sh "sed -i 's/PASSWORD/${params.PASSWORD}/g' ./image.yml"
    }
    stage('Add Grafana address IP to inventory file') {
        sh "sed -i 's/IP_GRAFANA/${params.GRAFANA_IP}/g' ./image.ini"
    }
    stage('Add Registry address IP to playbook file') {
        sh "sed -i 's/IP_REGISTRY/${params.REGISTRY_IP}/g' ./image.yml"
    }
    stage('Select image to playbook file') {
        sh "sed -i 's%IMAGES_PULL%${params.IMAGES_PULL}%g' ./image.yml"
        // On met des '%' car il peut y avoir un '/' dans l'image. Exemple : grafana/grafana:8.4.4
    }
    stage('Add image push to playbook file') {
        sh "sed -i 's/IMAGEREGISTRY/${params.IMAGESTOREGISTRY}/g' ./image.yml"
    }
    stage('Execute playbook') {
        sh "ansible-playbook -i ./image.ini ./image.yml"
    }
}