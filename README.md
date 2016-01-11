# hdome_dev
Developer support for Haplodome project

### Vagrant setup
- Requires Vagrant, VirtualBox, Ansible on your host machine
- Requires a copy of database data

Just run 'vagrant up' in the directory and load the database.

### Vagrant Database Setup
(To be automated at a later date)
TODO: Insert instructions here

### PyCharm setup
Do after vagrant has finished its provisioning step successfully!

[ Search for 'interpreter']
- Under Project Interpreter: add remote interpreter - e.g 
				vagrant instance folder is /Users/siriuz/Projects/hdome_dev/vagrant-hdome
				Python interpreter path is the python binary inside the vagrant machine's virtualenv

- Under Build, Execution, Deployment > Console > Python Console: add Python interpreter - e.g
				Python interpreter select the remove python that you set up above
				Working directory: select the app folder inside the vagrant directory

- Under Tools > SSH Terminal: Change connection settings to Default Remote Interpreter

[ Search for 'Django']
- Under Build, Execution, Deployment > Console > Django Console: set Python Interpreter to above
- Under Languages & Frameworks > Django: Enable Django Support

To check that everything is working, run > manage.py task
If no errors show up then everything's dandy and you can do a runserver 0.0.0.0:8080 to spin up the Django development server!

### Vagrant Tips

Vagrant commands are to be run in the same directory or subdirectory as your Vagrantfile

Vagrant up - starts up the virtual machine based on the Vagrantfile and runs whatever provisioning procedures in specified in the Vagrantfile. In the case of this project we use Ansible to provision the virtual machine. This sets up the Django project and its dependencies.

Vagrant halt - kills the vm

Vagrant suspend - pauses the vm (suspend state to disk)

Vagrant destroy - deletes the vm (!! all data on the vm is lost permanently !!)

Vagrant port - shows the ports that are being forwarded from the vm to localhost. Ports that are forwarded can be accessed at localhost:<host port>. These ports are specified in the Vagrantfile

Vagrant ssh - starts an SSH session into the vm 

Vagrant share - produces a publicly accessible URL to your running Vagrant box
