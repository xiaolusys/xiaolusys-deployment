node {
  properties([parameters([string(defaultValue: 'latest', description: '', name: 'commit_id')])])
  checkout scm
  sh("sed -ie 's/COMMIT_ID/${params.commit_id}/g' xiaolusys-deployment.yaml")
  sh("kubectl apply -f xiaolusys-deployment.yaml")
}

