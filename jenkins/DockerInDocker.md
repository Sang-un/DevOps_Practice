## docker sock 연결
sudo docker run \
    --name jenkins \
    -d \
    -p 8080:8080 \
    -p 50000:50000 \
    -v /home/jenkins/new:/var/jenkins_home \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -u root \
    jenkins/jenkins:lts

## docker jenkins 접속
docker exec -it <new_jenkins> bash

apt-get remove docker docker-engine docker.io containerd runc
## - Setup Repo
apt-get update
apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null
## - Install Docker Engine
apt-get update
apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin