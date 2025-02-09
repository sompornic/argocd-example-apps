# argocd-example-apps
### มาเริ่มกัน
-   install tool
    -   install minikube
        -   Mac
            -   brew install minikube
            -   minikube version
            -   minikube start
        -   Windows
            -   choco install minikube
            -   minikube version
            -   minikube start
        -   Windows dowload
            -   https://github.com/kubernetes/minikube/releases
    -   kubectl Mac
        -   brew install kubectl
        -   kubectl version --client
    -   kubeclt Windows
        -   choco install kubernetes-cli or scoop install kubectl
        -   kubectl version --client
    -   argocd
        -   kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
    -   helm
        -   Mac
            -   brew install helm
            -   helm version
        -   Windows
            -   choco install kubernetes-helm , scoop install helm or dowload https://github.com/helm/helm/releases

## เริ่มต้นจากการทำให้สามารถเข้าหน้าเว็บ argocd ให้ได้ก่อน 
-   forward-port arogocd ก่อน
    -   kubectl port-forward svc/argocd-server -n argocd 8080:443
    -   แล้วเข้า localhost:8080 in bowser user: admin ส่วน pass step ถัดไป
    -   kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 -d เพื่อแกะรหัาแล้วนำไปใช้ก็เป็นอันเข้าได้ล่ะ
    -   ทีนี้มาทำการ login argocd in cli เพื่อให้เราสั่งหรือดูของจาก cli ได้เลย command: argocd login localhost:8080 กด y ใส่ user pass เดียวกับ bowser
## ต่อมาเป็น helm 
-   การ create helm template
    -   ทำการ cd เข้าไปยัง project แล้วรันคำสั่ง: helm create ชื่อที่ต้องการตั้ง
-   สิ่งที่ควรตรวจสอบเกี่ยวกับ helm
    -   เช็คไฟล์ deployment , service ที่ default มาจาก template ถ้าไม่มั่นใจเอา deployment ที่เขียนแบบ fix value ไปก่อนได้เลยแล้วลอง apply file applicaition ของตัวที่เรียกไป repo ที่ทำ helm ไว้ หลังจากที่ app on ได้เเล้วเราค่อนมาใส่ตัวแปลที่ได้จากไฟล์ values.yaml