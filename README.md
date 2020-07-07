### k8s_customize_controller
### https://github.com/kubernetes/sample-controller 官方demo

``
kubectl proxy --port=8080
``
### k8s api规则:  apis/apiVersion/kind/name
如：
``
http://localhost:8080/apis/apiextensions.k8s.io/v1beta1/customresourcedefinitions/students.bolingcavalry.k8s.io
``

### 自定义controller只需要pkg/apis代码即可

### 执行以下命令，会先下载依赖包，再下载代码生成工具，再执行代码生成工作：
``
../../pkg/mod/k8s.io/code-generator/generate-groups.sh all \
k8s_customize_controller/pkg/client \
k8s_customize_controller/pkg/apis \
bolingcavalry:v1 \
--output-base "$GOPATH/src" \
--go-header-file $GOPATH/pkg/mod/k8s.io/code-generator/hack/boilerplate.go.txt 
``

### 在$GOPATH/src/k8s_customize_controller目录下，执行以下命令：
``
go get k8s.io/client-go/kubernetes/scheme \
&& go get github.com/golang/glog \
&& go get k8s.io/kube-openapi/pkg/util/proto \
&& go get k8s.io/utils/buffer \
&& go get k8s.io/utils/integer \
&& go get k8s.io/utils/trace
``

### 解决了包依赖问题后，在$GOPATH/src/k8s_customize_controller目录下执行命令go build，即可在当前目录生成k8s_customize_controller文件；
``
go build
./k8s_customize_controller -kubeconfig=$HOME/.kube/config -alsologtostderr=true
``