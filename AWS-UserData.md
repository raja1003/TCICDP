# TCICDP
implemented CI & CD pipeline

/////////////////////////////////////////////---START---//////////////////////////////////////////////////
AWS User Data Script
/////////////////////////////////////////////---START---//////////////////////////////////////////////////
sudo yum update -y
sudo yum install -y httpd
sudo systemctl start httpd.service
sudo systemctl enable httpd.service
EC2_AVAIL_ZONE=$(curl -s http://169.254.169.254/latest/meta-data/placement/availability-zone)
sudo echo "<h1>Hello World From Natraj at at $(hostname -f) in AZ '$EC2_AVAIL_ZONE' </h1>" > /var/www/html/index.html

#!/bin/bash
sudo yum update -y
sudo yum install -y httpd
sudo systemctl start httpd.service
sudo systemctl enable httpd.service
sudo echo "<h1> At $(hostname -f) </h1>" > /var/www/html/index.html

#!/bin/bash
sudo su
yum update -y
yum install -y httpd
systemctl start httpd.service
systemctl enable httpd.service
echo "<h1> At $(hostname -f) </h1>" > /var/www/html/index.html
crontab -l | { cat; echo "*/1 * * * * root 'date > /var/www/html/index.html"; } | crontab -
echo "*/1 * * * * ec2-user date --from-cron" >> /var/spool/cron/ec2-user

#!/bin/bash
yum update -y
yum install httpd php php-mysql -y
cd /var/www/html
echo "healthy" > healthy.html
wget https://wordpress.org/wordpress-5.1.1.tar.gz
tar -xzf wordpress-5.1.1.tar.gz
cp -r wordpress/* /var/www/html/
rm -rf wordpress
rm -rf wordpress-5.1.1.tar.gz
chmod -R 755 wp-content
chown -R apache:apache wp-content
wget https://s3.amazonaws.com/bucketforwordpresslab-donotdelete/htaccess.txt
mv htaccess.txt .htaccess
chkconfig httpd on
service httpd start

#!/bin/bash
yum update -y
aws s3 sync --delete s3://uourbucker-code1234 /var/www/html

yum install -y httpd mariadb-server
systemctl start httpd
systemctl enable httpd
usermod -a -G apache ec2-user
chown -R ec2-user:apache /var/www
chmod 2775 /var/www
find /var/www -type d -exec chmod 2775 {} \;
find /var/www -type f -exec chmod 0664 {} \;
echo "<?php phpinfo(); ?>" > /var/www/html/phpinfo.php

Print CPU Usage

ps -Ao user,uid,comm,pid,pcpu,tty -r | head -n 6
crontab

sudo su
crontab -u ec2-user -l
echo -e "*/1 * * * * ~/aws-scripts-mon/mon-put-instance-data.pl -mem-util --mem-used --mem-avail --swap-util --disk-space-util --disk-space-used --disk-space-avail --memory-units=megabytes --disk-path=/dev/xvda1 --from-cron " | crontab -u ec2-user -
exit

User Data Script to setup cloud watch

#!/bin/sh
yum install -y perl-Switch perl-DateTime perl-Sys-Syslog perl-LWP-Protocol-https perl-Digest-SHA unzip
cd /home/ec2-user
curl http://aws-cloudwatch.s3.amazonaws.com/downloads/CloudWatchMonitoringScripts-1.2.1.zip -O
unzip CloudWatchMonitoringScripts-1.2.1.zip
rm -rf CloudWatchMonitoringScripts-1.2.1.zip
chown ec2-user:ec2-user aws-scripts-mon
echo "* * * * * ec2-user /home/ec2-user/aws-scripts-mon/mon-put-instance-data.pl --mem-util --swap-util --aggregated --auto-scaling --from-cron" >> /var/spool/cron/ec2-user
echo "0 * * * * ec2-user /home/ec2-user/aws-scripts-mon/mon-put-instance-data.pl --disk-space-used --disk-space-avail --disk-space-util --disk-path=/  --aggregated --auto-scaling --from-cron" >> /var/spool/cron/ec2-user

Aws cron script

This is your userdata script (which will be run by ec2-init / cloud-init when the instance launches), it will create hourly, daily, weekly, monthly jobs for the instance :


#!/bin/sh
sudo -s # become root

echo "#!/bin/sh" >> /etc/cron.hourly/scriptname #no file extensions
echo "Your command" >> /etc/cron.hourly/scriptname
chmod 700 /etc/cron.hourly/scriptname

echo "#!/bin/sh" >> /etc/cron.daily/scriptname #no file extensions
echo "Your command" >> /etc/cron.daily/scriptname
chmod 700 /etc/cron.daily/scriptname

echo "#!/bin/sh" >> /etc/cron.weekly/scriptname #no file extensions
echo "Your command" >> /etc/cron.weekly/scriptname
chmod 700 /etc/cron.weekly/scriptname

echo "#!/bin/sh" >> /etc/cron.monthly/scriptname #no file extensions
echo "Your command" >> /etc/cron.monthly/scriptname
chmod 700 /etc/cron.monthly/scriptname

exit # get out of root

attach Internet Gateway to VPC

aws ec2 attach-internet-gateway --vpc-id "vpc-04168b9211b81203a" --internet-gateway-id "igw-0ad040e30d9ec0f50" --region us-east-1```

/////////////////////////////////////////////---END---//////////////////////////////////////////////////
Run Swagger Generate Spec inside a docker container

docker run --rm -it golang
go get -u github.com/go-swagger/go-swagger/cmd/swagger
git clone https://github.com/pdrum/swagger-automation /app && cd /app
swagger generate spec -o ./swagger.yaml --scan-models

/////////////////////////////////////////////---END---//////////////////////////////////////////////////
#!/bin/bash
sudo yum update -y
sudo yum install httpd -y
sudo echo "Test Page" > /var/www/html/index.html
sudo systemctrl start httpd
sudo systemctl enable httpd
/////////////////////////////////////////////---END---//////////////////////////////////////////////////
# awsscripts

natrajbontha@natrajs-mbp awsdynamodb % dotnet lambda
Amazon Lambda Tools for .NET Core applications (3.3.1)
Project Home: https://github.com/aws/aws-extensions-for-dotnet-cli, https://github.com/aws/aws-lambda-dotnet



Commands to deploy and manage AWS Lambda functions:

        deploy-function         Command to deploy the project to AWS Lambda
        invoke-function         Command to invoke a function in Lambda with an optional input
        list-functions          Command to list all your Lambda functions
        delete-function         Command to delete a Lambda function
        get-function-config     Command to get the current runtime configuration for a Lambda function
        update-function-config  Command to update the runtime configuration for a Lambda function

Commands to deploy and manage AWS Serverless applications using AWS CloudFormation:

        deploy-serverless       Command to deploy an AWS Serverless application
        list-serverless         Command to list all your AWS Serverless applications
        delete-serverless       Command to delete an AWS Serverless application

Commands to publish and manage AWS Lambda Layers:

        publish-layer           Command to publish a Layer that can be associated with a Lambda function
        list-layers             Command to list Layers
        list-layer-versions     Command to list versions for a Layer
        get-layer-version       Command to get the details of a Layer version
        delete-layer-version    Command to delete a version of a Layer

Other Commands:

        package                 Command to package a Lambda project into a zip file ready for deployment
        package-ci              Command to use as part of a continuous integration system.

To get help on individual commands execute:
        dotnet lambda help <command>

/////////////////////////////////////////////---END---//////////////////////////////////////////////////
