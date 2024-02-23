Step 1: Building and Pushing the sentiment-analysis-logic Image to Docker Hub
Start by building and pushing the sentiment-analysis-logic image to Docker Hub using the following commands:
docker build -f Dockerfile -t divyangam094/sentiment-analysis-logic .
docker push divyangam094/sentiment-analysis-logic

Step 2: Updating sa-logic-deployment.yaml
In the Google Cloud Shell, pull the sa-logic image, create its tag, and push it to the Container Registry. Then, edit the sa-logic-deployment.yaml file to use the updated image: gcr.io/carbon-scene-413621/divyangam094/sentiment-analysis-logic:latest
Deploy the updated sa-logic-deployment.yaml and service-sa-logic.yaml files from the Google Cloud Shell.

Step 3: Configuring sa-web-app to Use sa-logic Cluster IP
Obtain the Cluster IP of sa-logic and update the Dockerfile of sa-web-app:

ENV SA_LOGIC_API_URL http://CLUSTER_IP:5000
Replace CLUSTER_IP with the Cluster IP of sa-logic which was 10.92.12.129 in my case.

Step 4: Building and Pushing the sa-web-app Image to Docker Hub
Build and push the sa-web-app image to Docker Hub. Then, pull the image, change its tag, and push it to the Container Registry from the Google Cloud Shell.

Step 5: Updating sa-web-app-deployment.yaml
Update the sa-web-app-deployment.yaml file to use the updated image:
image: gcr.io/carbon-scene-413621/divyangam094/sentiment-analysis-web-app:latest

Step 6: Configuring Frontend to Use sa-web-app Load Balancer IP
Use the external load balancer IP address of sa-web-app to update the App.js file:
fetch('http://LOAD_BALANCER_IP/sentiment', {
Replace LOAD_BALANCER_IP with the load balancer IP address of sa-web-app which was 34.48.71.222:80 in my case 

Step 7: Building and Pushing the Frontend Image to Docker Hub
After running npm install and npm build, build and push the frontend image to Docker Hub. Then, pull the image, change its tag, and push it to the Container Registry from the Google Cloud Shell.

Step 8: Deploying sa-frontend-app
Deploy the sa-front-app-deployment.yaml file as well as service-sa-web-app-lb.yaml.

Step 9: Accessing the Application
Once deployed, the application will be accessible at the following URL: http://35.245.221.205/
