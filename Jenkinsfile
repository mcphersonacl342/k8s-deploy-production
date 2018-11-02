pipeline {
  agent {
    label 'kubegit'
  }
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Update production versions with latest versions from staging') {
      steps {
        container('kubectl') {
          sh "sed -i \"s#image: .*#image: `kubectl -n staging get deployment -o jsonpath='{.items[*].spec.template.spec.containers[0].image}' --field-selector=metadata.name=carts`#\" carts.yml"
          sh "sed -i \"s#image: .*#image: `kubectl -n staging get deployment -o jsonpath='{.items[*].spec.template.spec.containers[0].image}' --field-selector=metadata.name=catalogue`#\" catalogue.yml"
          sh "sed -i \"s#image: .*#image: `kubectl -n staging get deployment -o jsonpath='{.items[*].spec.template.spec.containers[0].image}' --field-selector=metadata.name=front-end`#\" front-end.yml"
          sh "sed -i \"s#image: .*#image: `kubectl -n staging get deployment -o jsonpath='{.items[*].spec.template.spec.containers[0].image}' --field-selector=metadata.name=orders`#\" orders.yml"
          sh "sed -i \"s#image: .*#image: `kubectl -n staging get deployment -o jsonpath='{.items[*].spec.template.spec.containers[0].image}' --field-selector=metadata.name=payment`#\" payment.yml"
          sh "sed -i \"s#image: .*#image: `kubectl -n staging get deployment -o jsonpath='{.items[*].spec.template.spec.containers[0].image}' --field-selector=metadata.name=queue-master`#\" queue-master.yml"
          sh "sed -i \"s#image: .*#image: `kubectl -n staging get deployment -o jsonpath='{.items[*].spec.template.spec.containers[0].image}' --field-selector=metadata.name=shipping`#\" shipping.yml"
          sh "sed -i \"s#image: .*#image: `kubectl -n staging get deployment -o jsonpath='{.items[*].spec.template.spec.containers[0].image}' --field-selector=metadata.name=user`#\" user.yml"
          sh "kubectl -n production apply -f ."
        }
      }
    }
    stage('DT Deploy Event') {
      steps {
        createDynatraceDeploymentEvent(
          envId: 'Dynatrace Tenant',
          tagMatchRules: [
            [
              meTypes: [
                [meType: 'SERVICE']
              ],
              tags: [
                [context: 'CONTEXTLESS', key: 'app', value: "carts"],
                [context: 'CONTEXTLESS', key: 'environment', value: 'production']
              ]
            ]
          ]) {
        }
        createDynatraceDeploymentEvent(
          envId: 'Dynatrace Tenant',
          tagMatchRules: [
            [
              meTypes: [
                [meType: 'SERVICE']
              ],
              tags: [
                [context: 'CONTEXTLESS', key: 'app', value: "catalogue"],
                [context: 'CONTEXTLESS', key: 'environment', value: 'production']
              ]
            ]
          ]) {
        }
        createDynatraceDeploymentEvent(
          envId: 'Dynatrace Tenant',
          tagMatchRules: [
            [
              meTypes: [
                [meType: 'SERVICE']
              ],
              tags: [
                [context: 'CONTEXTLESS', key: 'app', value: "front-end"],
                [context: 'CONTEXTLESS', key: 'environment', value: 'production']
              ]
            ]
          ]) {
        }
        createDynatraceDeploymentEvent(
          envId: 'Dynatrace Tenant',
          tagMatchRules: [
            [
              meTypes: [
                [meType: 'SERVICE']
              ],
              tags: [
                [context: 'CONTEXTLESS', key: 'app', value: "orders"],
                [context: 'CONTEXTLESS', key: 'environment', value: 'production']
              ]
            ]
          ]) {
        }
        createDynatraceDeploymentEvent(
          envId: 'Dynatrace Tenant',
          tagMatchRules: [
            [
              meTypes: [
                [meType: 'SERVICE']
              ],
              tags: [
                [context: 'CONTEXTLESS', key: 'app', value: "payment"],
                [context: 'CONTEXTLESS', key: 'environment', value: 'production']
              ]
            ]
          ]) {
        }
        createDynatraceDeploymentEvent(
          envId: 'Dynatrace Tenant',
          tagMatchRules: [
            [
              meTypes: [
                [meType: 'SERVICE']
              ],
              tags: [
                [context: 'CONTEXTLESS', key: 'app', value: "queue-master"],
                [context: 'CONTEXTLESS', key: 'environment', value: 'production']
              ]
            ]
          ]) {
        }
        createDynatraceDeploymentEvent(
          envId: 'Dynatrace Tenant',
          tagMatchRules: [
            [
              meTypes: [
                [meType: 'SERVICE']
              ],
              tags: [
                [context: 'CONTEXTLESS', key: 'app', value: "shipping"],
                [context: 'CONTEXTLESS', key: 'environment', value: 'production']
              ]
            ]
          ]) {
        }
        createDynatraceDeploymentEvent(
          envId: 'Dynatrace Tenant',
          tagMatchRules: [
            [
              meTypes: [
                [meType: 'SERVICE']
              ],
              tags: [
                [context: 'CONTEXTLESS', key: 'app', value: "user"],
                [context: 'CONTEXTLESS', key: 'environment', value: 'production']
              ]
            ]
          ]) {
        }
      }
    }
  }
}
