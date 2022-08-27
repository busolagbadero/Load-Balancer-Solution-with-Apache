 Launched Three RHEL8 Web Servers ,One MySQL DB Server (based on Ubuntu 20.04 ) ,One RHEL8 NFS server and One Apache-Loadbalancer (based on Ubuntu 20.04 ).
 
![oyr](https://user-images.githubusercontent.com/94229949/187030137-c1aa5f55-f3f7-4091-8cbf-9e7294295bd8.png)

Opened TCP port 80 on Apache-lb

installed apache and configured it to point traffic coming to LB to both Web Servers using these commands 'Install apache2
sudo apt update
sudo apt install apache2 -y
sudo apt-get install libxml2-dev


Enabled following modules:
sudo a2enmod rewrite
sudo a2enmod proxy
sudo a2enmod proxy_balancer
sudo a2enmod proxy_http
sudo a2enmod headers
sudo a2enmod lbmethod_bytraffic'


Restarted apache2 service so the change can take effect using command  ' sudo systemctl restart apache2 '

![oy1](https://user-images.githubusercontent.com/94229949/187030296-53ebff36-1c6d-44ea-a1ae-1a68015f49f9.png)

![oy2](https://user-images.githubusercontent.com/94229949/187030300-802283ac-5a6a-4389-802c-e49f6a63420a.png)

Made sure apache2 is up and running

![oyr1](https://user-images.githubusercontent.com/94229949/187030410-97ed9e0b-ac8b-4d43-9f28-8d942d9d26c2.png)

Configured load balancing 

![oy3](https://user-images.githubusercontent.com/94229949/187030449-d69bfbc9-6df5-48de-8ceb-a83bdbd1826d.png)

Verified that the configuration works by accessing the Load balancer public IP address http://3.93.219.154/admin_tooling.php

![oy4](https://user-images.githubusercontent.com/94229949/187030626-374207dc-e860-451b-8f0f-41a5cfca3281.png)

![oy5](https://user-images.githubusercontent.com/94229949/187030633-4f0cbce3-79d3-4d8c-bfa5-b6af0ce187a1.png)

Opened the terminals for Web Servers and ran the command 'sudo tail -f /var/log/httpd/access_log ' refreshed the browser page several times and made sure that both servers received HTTP GET requests from the LB – The new records appeared in each server’s log file.

![oyr2](https://user-images.githubusercontent.com/94229949/187030805-1057b893-0976-4063-a330-228e1417c059.png)

Configured Local DNS Names Resolution since there are lots of webservers under the load balancer using command  'sudo vi /etc/hosts '

![oy6](https://user-images.githubusercontent.com/94229949/187031016-06f52287-1c6c-459a-a231-87c29cb24ca6.png)

Updated  LB config file with 'web1 ' 'web2' and 'web3'  instead of IP addresses.

![oyr3](https://user-images.githubusercontent.com/94229949/187031125-11b3d168-c14a-4dc8-8b13-621f70147da4.png)

To check if it is working , Curl Web Servers from LB locally using command  'curl http://Web1 ' or 'curl http://Web2 ' and 'curl http://Web3 '  and it returned the html version of the website 

Local name resolution worked .

![oy7](https://user-images.githubusercontent.com/94229949/187031299-7af28b10-9f76-4989-b46a-e313e67e8490.png)

![oy8](https://user-images.githubusercontent.com/94229949/187031320-3382e57e-a468-458e-aaa1-6b989ce09b12.png)

![oy9](https://user-images.githubusercontent.com/94229949/187031332-e4462df4-3fe3-4d8b-a45a-69c926568ba8.png)



