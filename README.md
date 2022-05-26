# ANSIBLE-SETUP
**what is Ansible ?**

	Ansible is a configuration managment tool which is used for configuring the Node or salve machine through ssh.
	Ansible use the PUSH Based method to do configuration.
	Ansible dosent require the 3re party aggent to run on node.
	No s/w required on node system only need python installed.
	Ansible use the YAML language for writing the play.
	All the script is writen in playbook in the form of play.

**What is YAML ?**
		Full form og YAML is (yet another markup language) store the data in form of key or distonary: value or list.
		we can write multiple script in single YAML file.
		
		
**Sample:-**
		
			LIST- simple list eg- list of vegetable fruits color defined by - 
			---   (START of YAML file)
			# List of fruits
			-apple
			-banana
			-mango		
			... (END of YAML file)	
			---   (START of YAML file)			
			#Dictonary- key and value 
			Fname: Akshay
			Lname: Bhalkar	
			... (END of YAML file)
			---
			#List of dictonary and dictonary of list
			#list of fruits
			-apple
				name:apple
				color: red
				vatimin: A
				Country:       ( here Key has diff value )
					-India
					-Usa			(diff Value)
					-uk
			-banana 
				name: banana
				colour: Yello
				vatiminm: B 
				country: {inda,usa,england,brazil}      (key: value)
			...	
			---
			# Multi line value 
			address: |
				100,south pole
				usa
				wardha
						
			...
			
**cmd used in ansible 

			/etc/ansible/hosts -> hosas/nodes on which automation as to perform
			/etc/ansible/ansible.conf -> config file 
			
			#ssh cmd use 
			
				*ssh -i ansible-mumbai.pem centos@172.31.34.44 free 
				
			*ansible -i host all -u centos --private-key=id_rsa -m shell -a uptime
			*ansible -i host all -u centos --private-key=id_rsa -m ping 
			
				i -> inventory   (static and dynamic)
				u -> username
				m -> module 
				a -> argument
				
				
				
**Modules in ansible
 
			Module is nothing but configuration on server 
			
			ansible webservers -m service -a "name=httpd state=started"
			ansible webservers -m ping

			# config need to make at time of setup in ansibile.cfg file
			
			inventory= /root/hosts
			host_keychecking= false   ---- for key verification 
			remote_user= centos
			private-key_file=/root/id_rsa
			
			ansible is specially used for Patching and patching is nothing kernal update.			
			according to project we can create different config file and hosts file rather doing changes in /etc/ansible/ansbile.cfg it will easy to manage.
			
			*ansible -i hosts all -m shell -a hostname    -> hostname is module and run on shell 
			
			*Hosts file is nothing is but inventory
			
** Lets Write a playbook 

			#Before this keep the ansible.cfg , hosts file in project.
			
			Debug module is used to print the hello txt 
			---
			- name: Print some txt 
			  hosts: all
			  tasks:
				- debug:
					msg: "Hello world"
			...
						
						*ansibile-playbook playbook1.yaml
						
			# Also set alias for easy mnd like gp for git pull
			
				*vim /etc/profile
				
					alias gp='git pull origin master'
			