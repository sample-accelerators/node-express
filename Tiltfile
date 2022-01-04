allow_k8s_contexts(os.getenv("CURRENT_CONTEXT", default='kind-kind'))

NAMESPACE = os.getenv("NAMESPACE", default='default')

k8s_custom_deploy(
    'node-express',
    apply_cmd="tanzu apps workload apply -f config/workload.yaml " +
              " --namespace " + NAMESPACE +
              " --yes >/dev/null" +
              " && kubectl get workload node-express --namespace " + NAMESPACE + " -o yaml",
    delete_cmd="tanzu apps workload delete -f config/workload.yaml --namespace " + NAMESPACE + " --yes",
    deps=['package.json', 'server.js'],
)

k8s_resource('node-express', extra_pod_selectors=[{'serving.knative.dev/service': 'node-express'}])
