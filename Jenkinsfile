node {
  properties([parameters([string(defaultValue: 'latest', description: '', name: 'commit_id')])])
  checkout scm

  sh("sed -ie 's/COMMIT_ID/${params.commit_id}/g' xiaolusys-deployment.yaml")
  if (env.BRANCH_NAME == "staging") {
    sh("sed -ie 's/TARGET_NAME/k8s/g' xiaolusys-deployment.yaml")
    sh("kubectl apply -f xiaolusys-deployment.yaml -n ${env.BRANCH_NAME}")
  } else {
    sh("sed -ie 's/TARGET_NAME/k8s-production/g' xiaolusys-deployment.yaml")
  } 
  
  if (env.BRANCH_NAME == "production") {
    sh("kubectl apply -f xiaolusys-deployment.yaml -n ${env.BRANCH_NAME}")
    
    sh("sed -ie 's/TARGET_NAME/k8s-production/g' xiaolusys-defense-deployment.yaml")
    sh("sed -ie 's/COMMIT_ID/${params.commit_id}/g' xiaolusys-defense-deployment.yaml")
    sh("kubectl apply -f xiaolusys-defense-deployment.yaml -n ${env.BRANCH_NAME}")

    sh("sed -ie 's/COMMIT_ID/${params.commit_id}/g' celery-deployment.yaml")
    sh("kubectl apply -f celery-deployment.yaml -n ${env.BRANCH_NAME}")

    sh("sed -ie 's/COMMIT_ID/${params.commit_id}/g' celery-gevent-deployment.yaml")
    sh("kubectl apply -f celery-gevent-deployment.yaml -n ${env.BRANCH_NAME}")
    
    sh("sed -ie 's/COMMIT_ID/${params.commit_id}/g' celerybeat-deployment.yaml")
    sh("kubectl apply -f celerybeat-deployment.yaml -n ${env.BRANCH_NAME}")
  }

  if (env.BRANCH_NAME == "flower") {
    sh("sed -ie 's/COMMIT_ID/${params.commit_id}/g' flower-deployment.yaml")
    sh("kubectl apply -f flower-deployment.yaml -n ${env.BRANCH_NAME}")
  }
}

