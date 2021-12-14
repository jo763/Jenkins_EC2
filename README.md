![](diagrams/Jenkins_Diagram.png)

## Install Java onto the Jenkins EC2 instance server
- https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-on-ubuntu-18-04#installing-specific-versions-of-openjdk
## Install Jenkins onto the Jenkins EC2 instance server
- https://www.digitalocean.com/community/tutorials/how-to-install-jenkins-on-ubuntu-18-04
- Jenkins should now be working on the EC2 instance
## The execution shell script in Jenkins for the app instance
![](Videos/jenkins_app.gif)
```
rsync -avz -e "ssh -o StrictHostKeyChecking=no" app ubuntu@54.246.30.224:/home/ubuntu


ssh -A -o "StrictHostKeyChecking=no" ubuntu@54.246.30.224 <<EOF

# install git
#sudo apt-get install git -y
#rm -rf Shahrukh_eng99_CICD/

#git clone https://github.com/jo763/Shahrukh_eng99_CICD
# Change permission of provision to executable and then executing it
chmod +x /home/ubuntu/Shahrukh_eng99_CICD/environment/app/provision.sh
/home/ubuntu/Shahrukh_eng99_CICD/environment/app/provision.sh
cd /home/ubuntu/Shahrukh_eng99_CICD/app
sudo apt install npm -y
sudo npm install -y
echo 'export DB_HOST="mongodb://10.0.7.66:27017/posts"' >> .bashrc
#npm start
EOF
```


## The execution shell script in Jenkins for the database
![](Videos/jenkins_db.gif)
```
rsync -avz -e "ssh -o StrictHostKeyChecking=no" environment/ ubuntu@10.0.7.66:/home/ubuntu

ssh -A -o "StrictHostKeyChecking=no" ubuntu@10.0.7.66 <<EOF


# Change permission of provision to executable and then executing it
chmod +x /home/ubuntu/environment/db/provision.sh
/home/ubuntu/environment/db/provision.sh
##cd /home/ubuntu/Shahrukh_eng99_CICD/app
##sudo apt install npm -y
##sudo npm install -y
#npm start
# Allow members of group sudo to execute any command
EOF
```
