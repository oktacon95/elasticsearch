timestamps {

 node () {

  stage ('checkout repository') {
   checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'GitHub_User', url: 'https://github.com/oktacon95/elasticsearch']]]) 
  }
  stage ('build docker image') {
   sh "docker build -t myelasticsearch ." 
  }
  stage ('stop old docker image') {
   sh "docker stop elasticsearch" 
  }
  stage ('create new docker container') {
   sh 'docker run -d --rm -p 9200:9200 -p 9300:9300 -v /usr/share/elasticsearch/data:/usr/share/elasticsearch/data -u elasticsearch:root -e "discovery.type=single-node" -e "cluster.name=elasticsearch-cluster-schoolproject" --network elknet --name elasticsearch myelasticsearch'
  }
 }
}
