docker Installation
https://docs.docker.com/engine/install/ubuntu/

QUESTION : CONTAINERIZATION AND APPLICATION DEPLOYMENT WITH DOCKER 

1) LAUNCH AN LINUX/UNIX INSTANCE (I HAVE USED HERE THE UBUNTU 24.04 (NOBLE) INSTANCE FROM AWS).
2) ACCESS THE INSTANCE WITH SSH USING MOBAXTERM(OR CAN USE ANY OTHER S/W).
- OPEN MOBAXTERM -> CLICK ON SESSION -> CLICK ON SSH -> PASTE THE PUBLIC IP IN THE REMOTE HOST -> SPECIFY THE USERNAME(ubuntu/ec2-user) -> CLICK ON ADVANCE SETTINGS -> TICK THE USE PRIVATE KEY -> PROVIDE THE PRIVATE KEY. 
- THIS WILL CONNECT YOU TO YOURS INSTANCE (YOU CAN VERIFY BY USING THE PRIVATE IP).

3) INSTALL DOCKER ON THE INSTANCE USING (https://docs.docker.com/engine/install/ubuntu/)
- LOOK FOR INSTALL USING THE apt REPOSITORY
- # Add Docker's official GPG key:
sudo apt-get update

sudo apt-get install ca-certificates curl

sudo install -m 0755 -d /etc/apt/keyrings

sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc

sudo chmod a+r /etc/apt/keyrings/docker.asc

- # Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update

- To install the latest version, run:
- sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

4) CREATE A NEW DIRECTORY 
- mkdir docker
- cd docker

5) CREATE A FILE index.html
- echo "HELLO,DOCKER!" > index.html

6) CREATE A FILE NAMED dockerfile
- touch dockerfile
- ls

7) OPEN THE dockerfile IN TEXT EDITOR AND ADD THE FOLL:
- sudo vim dockerfile
- PRESS I(FOR INSERT MODE)

FROM nginx
COPY index.html /usr/share/nginx/html         (## THIS DOCKERFILE DEFINES A NEW DOCKER IMAGE THAT USES THE OFFICIAL NGINX IMAGE AS A BASE, THEN COPY THE index.html FILE TO APPROPRIATE LOCATION IN THE IMAGE).

- PRESS esc
- :wq!(TO SAVE AND QUIT)

8) START DOCKER AND BUILD DOCKER IMAGE FROM dockerfile

- sudo service docker status (## CHECK THE STATUS OF docker)

- IF IN STOP OR IN ACTIVE STATE USE (sudo service docker start) 

- docker build -t docker .   (## -t TAGS THE IMAGE WITH THE NAME 'docker').
  (## HERE docker IS THE FOLDER AND WE HAVE THE dockerfile INSIDE OF THE FOLDER).

- sudo docker images 

9) RUN THE DOCKER CONTAINER FROM THE IMAGE
- docker run -p 8080:80 docker  (## AFTER RUNNING THIS COMMAND YOU WILL BE PRESENT INSIDE YOUR CONTAINER)(THE COMMAND LINE WILL NOT BE ACCESSIBLE USE ctrl+c TO EXIT)(## THIS TELLS DOCKER TO RUN THE docker CONTAINER AND MAP PORT 8080 ON YOUR LOCAL MACHINE TO PORT 80 INSIDE THE CONTAINER).
- docker run -d -p 8080:80 docker (## THIS RUNS THE DOCKER CONTAINER IN DETACHED MODE).
- docker ps (## SHOWS THE RUNNING CONTAINERS).

10) ACCESS THE APP
- SINCE I HAVE USED THE AWS UBUNTU(24.04) INSTANCE, I WILL COPY THE INSTANCE PUBILC IP:8080
- THE CONTAINS FROM THE index.html PAGE ARE NOW VISIBLE IN THE BROWSER.

- docker stop container_id (## STOPS THE CONTAINER, IF YOU REFRESH THE PAGE YOU WILL SEE A MSG 'WEB PAGE NOT AVAILABLE').
- docker rm container_id (## REMOVES THE CONTAINER AND THE DOCKER IMAGE).
