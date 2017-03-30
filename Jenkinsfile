node {
  properties([parameters([string(defaultValue: 'latest', description: '', name: 'commit_id')])])
  checkout scm
  sh("sed -ie 's/COMMIT_ID/${params.commit_id}/g' xiaolusys-deployment.yaml")
  sh("kubectl apply -f xiaolusys-deployment.yaml -n ${env.BRANCH_NAME}")
  if (env.BRANCH_NAME == "production") {
    sh("sed -ie 's/COMMIT_ID/${params.commit_id}/g' celery-deployment.yaml")
    sh("kubectl apply -f celery-deployment.yaml -n ${env.BRANCH_NAME}")
  }
  if (env.BRANCH_NAME == "hekad") {
    sh("sed -ie 's/COMMIT_ID/${params.commit_id}/g' celery-deployment.yaml")
    sh("kubectl apply -f celery-deployment.yaml -n ${env.BRANCH_NAME}")
  }
  if (env.BRANCH_NAME == "statsd_exporter") {
    sh("sed -ie 's/COMMIT_ID/${params.commit_id}/g' celery-deployment.yaml")
    sh("kubectl apply -f celery-deployment.yaml -n ${env.BRANCH_NAME}")
  }
}

