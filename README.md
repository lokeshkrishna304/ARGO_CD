# ARGO_CD
HELPS IN SETTING UP AND DEPLOYING ON THE KUBERNETES CLUSTER

STEP1:
#create name space and deploy the argocd
$kubectl create namespace argocd
$kubectl apply -n argocd --server-side --force-conflicts -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

STEP2:
#convert the service of argocd from clusterIP to NodePort mode
$kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "NodePort"}}' 

Step3:
#find which port is accessed by the nodeport mode 
$kubectl get service -A
argocd        argocd-server                             NodePort    100.xx.xx.xx    <none>        80:31486/TCP,443:31559/TCP   26m
ports used here is 31486 & 31559

Step4:
#open these ports on the server(control plane) 
SG EDIT in the server add the above mentioned ports.

step5:
# Access the ARGOCD server 
https://<servers public ip>:<port opened for nodeport>
https://10.32.xx.xx:31486
