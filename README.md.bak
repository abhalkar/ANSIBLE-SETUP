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
		
		
	Sample:-**
		
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
			
	cmd used in ansible 

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
				
				
				
	Modules in ansible
 
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
			
	Lets Write a playbook 

			#Before this keep the ansible.cfg , hosts file in project.
			
			Debug module is used to print the hello txt 
			---
			- name: Print some txt 
			  hosts: all
			  tasks:
				- debug:
					msg: "Hello world"
			...
						
						ansibile-playbook playbook1.yaml
						
			# Also set alias for easy mnd like gp for git pull
			
					vim /etc/profile
				
					alias gp='git pull origin master'
					
** Varible in Yaml file 

	variable can use multiple time 
	
			we have two varibles:- 
						cmd line -> highest
						Local  -> Loval varibles has high priority than global    hisg
						files  -> moderate
						Global 	-> low
						host	-> very low
						

			---
- name: varible in yaml
  hosts: all
  tasks:
    - debug:
        msg: "www.google.com"

# By using varibles

----
- name: varible in yaml
  hosts: all
  tasks:
    - debug:
        msg: "www.google.com"

# By using varibles

---
- name: varible in yaml
  hosts: all
  tasks:
    - debug:
        msg: "www.google.com"

# By using varibles

- name: varible in yaml
  hosts: all
  vars:
    - url : "global.www.google.com"
  tasks:
     debug:
        msg: "{{ url }}"
        vars:
          url: "local.google.com"

- name: varible using again 
  tasks: 
    debug:
      msg: "{{ url }}"

- name: varibles uded global 
  tasks:
    debug:
      msg: "{{ url }}"

- name: print os distribution 
  debug:
    msg: "{{ ansible_distribution }}"
    
- name: print os ipv4
  debug:
    msg:  "{{ ansible_lo.ipv4.address}}"
...


# We can also use ignore error which if one task is not required

- name: print os ipv4
  debug:
    msg:  "{{ ansible_lo.ipv4.address}}"
  ignore_errors: yes 
			
			
# AGENDA FOR ANSIBLE

-register varible ?

			we can store value in variable. EG- when we want to store any output that time we will use register variables
			Ansible register is a way to capture the output from task execution and store it in a variable
			
$ Example
	
	
	- name: register variable demo
	  hosts: all
	  tasks:
		- name: get uptime
		  shell:
			cmd: uptime
		  register: ut                              ---------> here ut is register varible where the valu will get stored after exicution.

		- name: print uptime  
		  debug:  
			msg: " the uptimeis is {{ ut.stdout }}" 
		
		
		
-conditions ?
			
			**if --> else  eg:- if java is avilable then only install Tomcat
				
			eg:- if os is centos then install httpd 
				 if os is ubantu then install apache2
				 
				 ansible -i hosts all -m setup
Exmaple:- 
				 
	- name: condition demo 
	  hosts: all
	  tasks:
	  - name: Readhat
		debug:  
			msg: "This is Redhat family"
		when: ansible_distribution_file_variety == "Redh]Hat"             --> condition  when family is ReadHat then print above msg 
	  - name: Debian
		debug:
			msg: "This is Debain family"
		when: ansible_distribution_file_variety == "Debian"    

# using the AND OR condtion 

AND (T + T = T)
		
	- name: condition demo 
	  hosts: all
	  tasks:
		- name: Readhat
		  debug:  
			msg: "This is Redhat family"
		  when: ansible_distribution_file_variety == "Redh]Hat" and ansible_distribution == "CentOS"                -> if both condition satisfies then only print above msg  (t+t=t)
	
	
OR (T + F = T) if (F + F = F)

	- name: condition demo 
	  hosts: all
	  tasks:
		- name: Readhat
		  debug:  
			msg: "This is Redhat family"
		  when: ansible_distribution_file_variety == "Redh]Hat" or ansible_distribution == "CentOS"       -> if any one is false then ok but both are false then false hence skiiping
	
	
# LOOPS IN ANSIBLE

		LOOPS is nothing but no of statement which are exicuting repitately called as loop. Contineously cycle 
		in loops need to provide the list the count of list times the loop will exicute.
		
	EXAMPLE:-
	
	- name: Example for loops demo
	  hosts: all
	  tasks:
		- name: print loop
		  debug:
			msg: "{{ item }}"                -> item will be varible
		  loop:
			- banana
			- mango
			- straberry
			- apple
		
		eg:- multiple pkg need to install we can use loop 
			
# tags 

		Tags are used to identify the task.

		if we have 4 tasks and we ant to add one task to another
		
		
	EXAMPLE:- 
	
	- name: tages demo 
	  hosts: all
	  tasks: 
	  - name: print redhat 
		debug: 
		  msg: "This is readhat"
		tags:
		  - readhat
	  - name: print Ubantu
		debug:
		  msg: "This is ubantu"
		tags:
		  - ubantu
	  - name: print Debian
		debug:
		  msg: "This is debian"
		tags:  
		  - debian 
	  
	  
	$ ansible-playbook tags.yml --skip-tags=ubantu

		This will skip the ubantu tasg and display only reamining
	
# Privilage-escalation 

			local user doesnt not have access to install pkges so we need to use SUDO this sudo is nothning but the privilage escalation.
			We will use become true becasue we need to run dmidecode as sudo user local user dont have permisiion.or we can edit this in ansible.cfg
			
EXAMPLE:- 
	
	- name: privilage-escalation demo 
	  hosts: all
	  become: true
	  tasks:
		- name: exicute dmidecode
		  shell:
			cmd: /sbin/dmidecode
		  register: out
		- name: print output
		  debug: 
			msg: "{{ out }}"
		

	
			