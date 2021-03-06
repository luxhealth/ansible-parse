# ansible-parse
Ansible scripts for end to end setup of a parse server also ready for migration and production

The scripts here follow the steps in [How To Host Parse Server tutorial series][1] by Brennen Bearnes from DigitalOcean Community.

## What you get
At the end you will get a server with the followings installed:
  * TLS/SSL enabled Mongodb Server
  * TLS/SSL enabled Parse Server
  * Parse Dashboard

## What you need
Before starting you need:
  * ansible installed workstation (i.e. your laptop)
  * an Ubuntu14.04 server with root access (i.e. a droplet from Digital Ocean)
  * A domain name pointing at the server

### How to install Ansible 

It is easy! Check this page: http://ansible-tips-and-tricks.readthedocs.io/en/latest/ansible/install/

Tested with Ansible version 2.1.1. So it is recommended!

### Sign up DigitalOcean

The scripts have no dependency on DigitalOcean, you can use any cloud provider. 

But DigitalOcean is a great choice for developers, like us!

If you do not have an account, you can register with my [referal link][2] and start with a $10 credit.

# Steps
## Step 0 - Prepare workspace

1. Clone this repository:

```
git clone https://github.com/turkenh/ansible-parse.git
```

2. Get submodules

```
cd ansible-parse
git submodule init 
git submodule update
```

3. Install dependencies

```
ansible-galaxy install -r requirements.yml
```

## Step 1 - Create Instance 

Create an Ubuntu 14.04 64 bit droplet on DigitalOcean and copy its ip.

![Step 1 - Create Instance](docs/create_instance.gif?raw=true "")

## Step 2 - Update Domain Record 

Update domain record with that ip for the domain you intend to use. (Make sure you set digitalocean nameservers from your domain providers control panel before)

![Step 2 - Update Domain Record](docs/domain_reg.gif?raw=true "")

## Step 3 - Run Ansible Part 1: Prepare For Migration

Edit group_vars/all file for yourself and update hosts file with the ip of your droplet. Then run "ansible-playbook setup-parse.yml"

![Step 3 - Run Ansible Part 1: Prepare For Migration ](docs/run_ansible_p1.gif?raw=true "")

![mongo conn](docs/endofp1.png?raw=true "Mongodb connection string")

## Step 4 - Start Migration

Copy the mongodb conn string in the previous step and start migration for your app on Parse.com

![Step 4 - Start Migration ](docs/start_migration.gif?raw=true "")

## Step 5 - Run Ansible Part 2: Complete Installation 

Go back to terminal where you started ansible installation and press "enter" to continue.

![Step 5 - Run Ansible Part 2: Complete Installation ](docs/run_ansible_p2.gif?raw=true "")

## Step 6 - Verify Installation & Data 

Go to \<your_domain_name\>:4040 and enter "admin/admin" (unless you changed it with parse_dashboard_user and parse_dashboard_password variables). Once you are ok with the data, go back to parse.com and finalize migration.

![Step 6 - Verify Installation & Data ](docs/verify.gif?raw=true "")

[1]: https://www.digitalocean.com/community/tutorial_series/how-to-host-parse-server
[2]: https://m.do.co/c/9bb7ed4991c1
