# SRE introduction
## Cloud Computing with AWS
### SDLC stages
#### Risk factors with SDLC stages
##### Monitoring

### Key Advantages:
- Flexibility
- Robustness
- Ease of use
- Cost


**SRE introduction**
- What is the role of SRE?
	- SREs are responsible for the reliability of a service
	- They ensure that a service is tested in all potential scenarios, and that risks and errors are identified early (ideally before the customer notices) and resolved quickly and smoothly
	- They help to make a business's service more flexible, more robust, easier to use, and more cost-effective


**Cloud Computing**
- What is Cloud Computing and the benefits of using it?
	- Cloud Computing is the renting of a cloud computing company's servers.
	- Benefits:
		- It's cheaper for companies to only pay for the servers they use than to buy their own
		- The company can monitor their service live
		- The company can stress-test a service to make sure it can handle extreme cases, e.g. more users than expected


**What is Amazon Web Services (AWS)**
- What is AWS and benefits of using it
	- AWS is a provider of on-demand cloud platforms
	- Benefits:
		- Pay-as-you-go
		- Easy to scale up/down based on your needs - auto-scale
		- AWS take care of the care required to keep a physical server running efficiently


**What is SDLC and stages of SDLC**
- What is SDLC and what are the stages of it?
	- The Software Development Life Cycle is the series of steps that are involved in developing working, robust software
	- Stages:
		- Planning
		- Design
		- Building
		- Testing
		- Deploying
		- Maintaining


**What are the Risk levels at each stage of SDLC?**
- LOW
- MEDIUM
- HIGH
	- Planning: LOW
	- Design: LOW
	- Building: LOW/MEDIUM
	- Testing: LOW/MEDIUM
	- Deploying: HIGH
	- Maintaining: HIGH


**Software Development Cycle**
![Software Development Cycle](software_development_cycle.png)


**On Premises Storage**
- This means that the company has its own physical servers and data centre for their service
- Pros:
        - The company can be fully responsible for the security and upkeep of the servers and data - they are not relying on another business
	-
- Cons:
        - May not be cost-effective, depending on how close the estimation of traffic and storage space required is to how the service is actually used
	- A lot of expenses are required to keep the servers and data centre running, e.g. hiring security guards, buying servers, building physical storage for the servers and data centre, etc.


![On Premises Storage](on_premises_storage.jpg)


**Cloud Storage**
- This means that the company rents servers from a cloud computing company instead of buying their own
- Pros:
        - Can scale up or down as the service requires -> flexible
	- Reduces costs as the company is only paying for the servers and space the service requires
- Cons:
        - May not be suitable for sensitive data which needs to be protected in accordance with legislation/company procedure
	- Relying on the cloud computing company to keep the servers running and secure

![Cloud Storage](cloud_storage.gif)


**Hybrid Cloud Storage**
- This means that the company rents servers for the data they want to be publicly available, but has its own physical servers and data centre for data that needs to be kept private and secure
- Pros:
        - The company can choose which data to make public, and can take on responsibility for protecting more sensitive data so they have better control over who has access to it
- Cons:
        - More expensive than migrating fully to the cloud

![Hybrid Cloud Storage](hybrid_cloud_storage.jpg)


**Multi Cloud Storage**
- This means that the company keeps multiple copies of their data and servers with different cloud providers so that the service can still run if one of the providers' service is down
- Pros:
	- Servers and data are backed up
	- Service can continue uninterrupted if one of the servers is down, as the company can switch to another server that is functional
- Cons:
	- More expensive than having one copy as the company needs to pay each extra cloud provider they use, on top of the main one

![Multi Cloud Storage](multi_cloud_storage.png)


![Vagrant Diagram](vagrant_image.png)


**To Set Up NginX Web Server On Virtual Machine**
- Make a Vagrantfile with the following text:
Vagrant.configure("2") do |config|
		config.vm.box = "ubuntu/xenial64"
		config.vm.network "private_network", ip: "192.168.10.100"
end
- in git bash, in the same directory as your Vagrantfile, enter the following commands:
	vagrant up
	vagrant ssh
- then use the following:
	sudo apt-get update -y
	sudo apt-get upgrade -y
	sudo apt-get install nginx -y
- to check whether the nginx package installed, use:
	systemctl status nginx
- then, in your browser, type in the ip address from the Vagrantfile (192.168.10.100)


**Tasks**
1. Create provision.sh script (in git bash) with the following lines:
	!#/bin/bash
	sudo apt-get update -y
	sudo apt-get upgrade -y
	sudo apt-get install nginx -y
	- Save and close, then run the following in git bash:
		chmod +x provision.sh
2. Inject the provision.sh script inside the Vagrantfile
	- add the following line in the Vagrantfile before the 'end' line
		config.vm.provision "shell", path: "provision.sh"
3. With vagrant up, Vagrantfile should run the script
4. Check 192.168.10.100 in the browser
