# cosbuddy
    Calling all cosplayers together!

# VM setup
    - Download xubuntu from https://xubuntu.org/download/
	- Download Virtualbox and the extension pack from https://www.virtualbox.org/wiki/Downloads
	- Install Virtualbox and then install the extension pack

## Creating the VM
    - Open Virtualbox and click on the blue exploding icon labelled as "New"
	- In name write projectone
	- Choose Linux as type
	- Choose Ubuntu (64-bit) as version (or Xubuntu 64-bit if available)
	- Click Next
	- Set 8192MB as the Memory Size and then click Next
	- Set "Create a virtual hard disk now" when configuring Hard disk and then click Create

## Configuring VM once the VM is created
    - Click on the name of your VM and then click on the cog icon labelled "Settings"
	- Under "General" settings click on "Advanced" tab and set "Bideractional" for "Shared Clipboard" and Drag'n'Drop
	- Under "System" settings click on "Processor" tab and set the Processor(s) slider between the green and the red section
	- Under "Display" settings click on "Screen" tab and set Video Memory to max

## Installing Xubuntu OS
    - Always from "Settings" go to "Storage" settings click on empty and then click on disk icon with dropdown
	- Click on "Choose disk file..." and select the xubuntu .iso file
	- Close the settings window
	- Click on "Start" and wait for the VM to boot up and start the OS installation
	- Once the window is up and the VM is booted up click on "Install Xubuntu"
	- Choose your keyboard layout click Continue
	- Flag both checkboxes under Updates and other software click Continue
	- Installation type "Erase disk and install Xubuntu"
	- Continue
	- Compile form and install
	- When finished click on Restart
	- When the message "Please remove the installation medium, then press ENTER: " appears just press ENTER
	- Once it finished loading you're done!

## Installing Guest Additions CD images...
    - On top of the window of the VM click on "Devices" and then click on "Insert Guest Additions CD image..."
	- A window will open
	- Right click inside the window and then open a terminal
	- write: "sudo ./autorun.sh" and then ENTER
	- restart VM

## Remove annoying password request when running a command on terminal
	- Open a terminal
	- run: "sudo nano -w /etc/sudoers"
	- enter password one last time
	- go to the line that says "%sudo ALL=(ALL:ALL) ALL" and change it to "%sudo ALL=(ALL:ALL) NOPASSWD:ALL"
	- then Ctrl+X -> Shify + Y -> Enter
	- you're good to go

## Install Jetbrains toolbox and IDEs
	- Download Jetbrains Toolbox from https://www.jetbrains.com/lp/toolbox/
	- go to Downloads folder and extract using command tar -xvf {filename with extension}
	- go into the extracted folder open a terminal from there and run the executable
	- once the Jetbrains cube appears log in
	- install IntelliJ IDEA Community Edition

## Install VSCode
    - Open terminal
    - Run: sudo snap install code --classic

## Install Java 17
    - Open terminal
    - Run: 
     sudo apt-get upgrade
     sudo apt-get update
     sudo apt install openjdk-17-jdk openjdk-17-jre

## Install Postgres
    - Open terminal
    - cd to configurations/database
    - run ./postgres-install.sh

## Setup DBs
### DB name list
	- gatherinservice
	- socialservice
	- gatewayservice
	- authservice

### Create your user
	- run in terminal
	- sudo -u postgres psql
	- CREATE USER {username} WITH PASSWORD {password} CREATEDB;

### Create DBs and grant privileges (Repeat these steps for each DB on list above)
	- run in terminal
	- sudo -u postgres psql
	- CREATE DATABASE {dbname};
	- GRANT ALL PRIVILEGES ON DATABASE {dbname} to {username};
	- \c {dbname}
	- GRANT ALL ON SCHEMA public TO {username};

## Install Firefox
    - Open terminal
    - Run:
     sudo apt install firefox

## Install Maven
	- Open terminal
	- Run:
	- sudo apt install maven
    
## Install Git & Setup Git credentials
    - Open terminal
    - Run:
     mkdir Projects
     cd Projects
     sudo apt install git
     git config --global credential.helper store
     git config --global user.email "{email}"
     git config --global user.name "{name}"
     git clone --recurse-submodules https://github.com/jdsinniah/cosbuddy.git

# Project startup
	- Open terminal from cosbuddy folder
	- cd common
	- mvn clean install

## Setup GitHub CLI
	- Open terminal and run:
	- sudo snap install gh
	- sudo apt-get install libcurl4-openssl-dev
	- gh auth login
	- And then follow instructions

## Install curl
	- Open terminal and run: sudo apt install curl

## Install NVM and Node
	- Open terminal and run:
	- curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
	- the close and reopen terminal and run:
	- nvm install --lts

# DEVELOPMENT HELPERS

## Git Utility
## Adding new submodule to cosbuddy project
    - Create first a repository in GitHub and copy the https url
    - Then open terminal and cd to cosbuddy folder
    - Run:
    - git submodule add {submodule url} ./{submodule name}
    - git commit -m "Added {submodule name} as git submodule to cosbuddy project"
    - git push

## Creating a new repository from GitHub CLI
	(DOCS JUST IN CASE https://docs.github.com/en/migrations/importing-source-code/using-the-command-line-to-import-source-code/adding-locally-hosted-code-to-github)
	- Open terminal and run:
	- gh repo create

## Clone cosbuddy project with submodules
    - git clone --recurse-submodules https://github.com/jdsinniah/cosbuddy.git

## Liquibase
## Adding a changelog
	- Create a changelog file in resources/db/changelog naming it with the following convention: db.changelog-ddmmyyyyhhmm-username.xml (hhmm uses military time)
	- Include the file within db.changelog-master.xml using <include file="{file path}"> tag
