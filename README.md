##### Local requirements:
* ansible >= 2.2.0  
* python >= 2.6  
* dopy  

##### How to run:
* Open the file `config.cfg` in your favorite text editor and change variables. At least you should change `server_name`, and specify users in `users` list.
* Start to deploy and follow the instructions: 
```
ansible-playbook deploy.yml -e "provider=cloud"
```
* When the process is done, you can see `.mobileconfig` files and certificates in the directory - `configs`. Send `.mobileconfig` to your users for using on iPhones or MacOS or send certificates for using on other clients (StrongSwan client for Android or native IKEv2 client for Windows)

* When the deploy proccess is done a new server will be placed in the local inventory file - `inventory_users`

* If you want to add or delete users, just update the (`users`) list in the config file (`config.cfg`) and then run the playbook:  
(This command will update users on all your servers in the file `inventory_users`, if you want to limit servers, you can use option `-l` )
```
ansible-playbook users.yml -u root -i inventory_users
ansible-playbook users.yml -u root -i inventory_users -l vpnserver.com
```

#### EC2:
* How to use Algo on EC2

* Setup AWS key env variables.
declare -x AWS_ACCESS_KEY_ID="XXXXXXXXXXXXXXXX"
declare -x AWS_SECRET_ACCESS_KEY="XXXXXXXXXXXXX"

* Deploy to EC2
ansible-playbook deploy.yml -e "provider=ec2"

* EC2 instances are added to inventory_users and can be used as described above with the exception of the user.

ansible-playbook users.yml -u ubuntu -i inventory_users

Currently EC2 dynamic inventory is not used for user management. This may be subject to change in the near future.


