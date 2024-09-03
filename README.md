![Capture d'écran 2024-09-03 161033](https://github.com/user-attachments/assets/3de18bbd-ae2c-4bca-8996-1e8de6b3e0ac)![Capture d'écran 2024-09-03 161033](https://github.com/user-attachments/assets/d4cb94fb-1941-435c-a8a0-da34d968cac1)![Capture d'écran 2024-09-03 223647](https://github.com/user-attachments/assets/612ba0cb-8080-4f72-b864-0e18cf86bdb6)The main idea is to : trigger manually the pipeline from jenkins , which will build , test and deploy the app to EKS cluster , the build stage will build the app into docker image and push it to dockerhub and which will be later pulled by the deployment file . to obtain finally the app on EKS cluster :

![image](https://github.com/user-attachments/assets/e0ea38dc-ee33-4df3-ab96-ce2c289d8e85)

the app : https://github.com/Aymen-thabet/simple-java-app

First thing to do is to create an EKS cluster with an attached role that have permissions to use EKS ressources : 

![Capture d'écran 2024-09-03 143223](https://github.com/user-attachments/assets/e0ed8640-81cb-4291-aeba-14b47409aaf4)

![Capture d'écran 2024-09-03 223647](https://github.com/user-attachments/assets/83217047-06a3-4a66-b41b-f68db95bfde8)


Then install pipeline: AWS Steps Plugin on your jenkins server :

![Capture d'écran 2024-09-03 143904](https://github.com/user-attachments/assets/96e83ea5-4bd1-4ebf-994c-7b0732040bed)

Now we need to set credentials so that my Jenkins server can acces dockerhub(to push image) and can acces to the cluster : 

![Capture d'écran 2024-09-03 140333](https://github.com/user-attachments/assets/0966264b-6d01-4a50-b910-37d86c3d026c)

![Capture d'écran 2024-09-03 143400](https://github.com/user-attachments/assets/e8e8adb2-f315-4d8a-bfb5-2c313901958c)

*setting up docker username and password*

Setting up credentials for the user to acces EKS and manage AWS ressources : 

![Capture d'écran 2024-09-03 145553](https://github.com/user-attachments/assets/a514f2b0-b2b3-47f7-97aa-26cc45344912)

![Capture d'écran 2024-09-03 145611](https://github.com/user-attachments/assets/5b857072-9ea2-462b-8eaa-a5674c3ec5b7)

![Capture d'écran 2024-09-03 145635](https://github.com/user-attachments/assets/e2d7dec0-9328-4349-ae9f-2933d477cc77)

Now we take the credentials ID from the credential of AWS to put it in the jenkins file push stage : 

![Capture d'écran 2024-09-03 153401](https://github.com/user-attachments/assets/396e3ccf-a079-4d73-b350-cdcb24544a62)

![Capture d'écran 2024-09-03 153530](https://github.com/user-attachments/assets/f656b859-f9fb-4ad8-b4c0-3b9e0e6f6aa0)

Now setting up the credential ID for the deployment stage : 

![Capture d'écran 2024-09-03 161033](https://github.com/user-attachments/assets/ccf8c497-f9e3-4068-9120-69a2986aed7d)

Now that we have all credentials set up , we manually build the pipeline : 

![Capture d'écran 2024-09-03 221639](https://github.com/user-attachments/assets/6e3bcc9a-615f-4f55-a5d9-cf400c335731)

![Capture d'écran 2024-09-03 221657](https://github.com/user-attachments/assets/b31c7101-430d-4d53-899e-d9f0faa212b8)
*building docker image*

![Capture d'écran 2024-09-03 221714](https://github.com/user-attachments/assets/8e2a0f28-dff8-45c2-b67d-55e58d64a568)
*login to dockerhub with credentials to push image*

![Capture d'écran 2024-09-03 221738](https://github.com/user-attachments/assets/dd0883cc-3531-4745-a9dc-3a523303b007)
*pushing image*

![Capture d'écran 2024-09-03 222658](https://github.com/user-attachments/assets/6b41d9e6-1684-41b0-9a6e-7c75c21d41ca)
*deployment of the app to EKS*

Finally , a pod is created in the EKS cluster !

![Capture d'écran 2024-09-03 222713](https://github.com/user-attachments/assets/61acb725-5980-4820-a80f-cd9a7ffcbc1d)
*Success*

This is a screenshot of the Jenkinsfile :

![Capture d'écran 2024-09-03 222948](https://github.com/user-attachments/assets/eabef5d8-b689-4b30-a300-524f5cfd3b75)

