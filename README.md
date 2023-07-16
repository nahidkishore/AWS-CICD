
## Setup a CodeDeploy agent to deploy code on EC2 Install the CodeDeploy agent:

You need to install the CodeDeploy agent on your Ubuntu EC2 instance. The CodeDeploy agent is a software package that runs on your instance and interacts with CodeDeploy to deploy your application.

### You can install the CodeDeploy agent by running the following script on your EC2 instance:
  
   
   
    #!/bin/bash 
    # This installs the CodeDeploy agent and its prerequisites on Ubuntu 22.04.  
    sudo apt-get update 
    sudo apt-get install ruby-full ruby-webrick wget -y 
    cd /tmp 
    wget https://aws-codedeploy-us-east-1.s3.us-east-1.amazonaws.com/releases/codedeploy-agent_1.3.2-1902_all.deb 
    mkdir codedeploy-agent_1.3.2-1902_ubuntu22 
    dpkg-deb -R codedeploy-agent_1.3.2-1902_all.deb codedeploy-agent_1.3.2-1902_ubuntu22 
    sed 's/Depends:.*/Depends:ruby3.0/' -i ./codedeploy-agent_1.3.2-1902_ubuntu22/DEBIAN/control 
    dpkg-deb -b codedeploy-agent_1.3.2-1902_ubuntu22/ 
    sudo dpkg -i codedeploy-agent_1.3.2-1902_ubuntu22.deb 
    systemctl list-units --type=service | grep codedeploy 
    sudo service codedeploy-agent status
