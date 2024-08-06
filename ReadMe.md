# ISE API and Automation Setup
To begin setting up your workstation for APIs, you need to install a few packages.

# Windows 10 and 11
# Install Windows Terminal
For a feature-rich terminal application on Windows, you can't get much better than the Windows Terminal.  This is _not_ the Windows Command Prompt, but is a single terminal application that allows you to access Command Prompt, PowerShell, and Azure CLI from a single window within tabs.  Once you install WSL, you can also access your Linux distribution from this application with full bash shell capabilities.

[Install and get started setting up Windows Terminal](https://learn.microsoft.com/en-us/windows/terminal/install)

# Install Windows Subsystem for Linux (WSL)
Follow the steps in [How to install Linux on Windows with WSL](https://learn.microsoft.com/en-us/windows/wsl/install) to install WSL on your Windows machine.  Microsoft has simplified the installation process over the years and is now a single command to enable all the prerequisites and install Linux (including your choice of Linux Distribution).

# Install VS Code (or VS Codium)

VS Code is offered by Microsoft and can be downloaded from https://code.visualstudio.com/<br>
VS Codium is a community-driven, freely-licensed binary distribution of Microsoft’s editor VS Code that can be downloaded from https://vscodium.com/

VS Code is a coding and file editor with GitHub controls.  You can view and edit files from any language with VS Code with the quick installation of Extensions.

## Supported Platforms for VS Code
VS Code is supported on the following platforms:

- Windows 10 and 11 (64-bit)
- macOS versions with Apple security update support. This is typically the latest release and the two previous versions.
- Linux (Debian): Ubuntu Desktop 20.04, Debian 10
- Linux (Red Hat): Red Hat Enterprise Linux 8, Fedora 36
> |💡| **Note:** | VS Code is a graphical interface.  If running a linux workstation, you need a desktop version of Linux.<br>If using WSL on Windows, install VS Code in Windows.  You can invoke VS Code from WSL and the Windows application will start.
> |---|---|---|

To invoke VS Code from your terminal:
1. `cd` into your working directory (project folder)
2. Type `code .` and press Enter.  The period matters.  It tells VS Code to open the current directory<br>
  a. for VS Codium, Type `codium .` and press Enter.  Again, the period matters.  It tells VS Codium to open the current directory

## Recommended Extensions
These extensions are recommended for the purpose of Ansible Automation.  Since Ansible uses YAML files for their playbooks and configurations, it is important that you have a powerful editor for these files. 
- YAML
- Prettier - Code Formatter
- Pretty TypeScript Errors

* * *
* * *
From this point forward, the commands shown will be in the bash shell of your Linux distribution/macOS Terminal.  Since WSL used Debian-based Linux distributions, all commands _should_ work.<br>
For macOS, a different package manager is used.  Homebrew is the most popular one at the time of this writing.  When you see an `apt` command, relace it with the `brew` command.

# Install cURL
cURL, which stands for client URL, is a command line tool that developers use to transfer data to and from a server. At the most fundamental, cURL lets you talk to a server by specifying the location (in the form of a URL) and the data you want to send.  This is how you will target the API requests to your specific destination.
```
sudo apt install -y curl
```

# Install git
To clone a `git` repository, 
Install the `git` utility
```
sudo apt install -y git
```

Install the basic files from the repository for this lab using the git clone repository command:
```
git clone https://github.com/ISEDemoLab/ISE_API_and_Automation_Setup
```

Change directories into `ISE_API_and_Automation_Setup` directory and `ls` to see the files from the repository on your workstation!
```
cd ISE_API_and_Automation_Setup/
ls
```

# Install Python3
Install the latest version of Python 3.x :
```
sudo apt install -y python3
```
> ⚠️ Use python3 and not python! Using python will install the outdated Python 2.x version.

Verify your new or updated Python version :
```
python3 --version
```
The Linux operating system can dynamically download and install software in the form of packages with the apt utility as you have seen.  Python has a similar capability using the pip utility ("Pip Installs Python") to install software packages. You must install the pip functionality first.

```
sudo apt install -y python3-pip
```

Install the virtual pip environment
```
pip install pipenv
```
> ⚠️ If you are using a version of Ubuntu older than 22.04 and get errors with this command, use the one below.
> 
```
sudo apt install -y pipenv
```

# Install Ansible
Install the package for adding Linux repositories
```
sudo apt-get install software-properties-common
```

Add the repository for **Ansible PPA (Personal Package Archive)**. A PPA is for non-standard software/update and generally used by people who want the latest and greatest.
```
sudo apt-add-repository ppa:ansible/ansible
```

The Ansible installation will take several minutes for all the requirements to download and install :
```
sudo apt install -y ansible
```

Verify your version of Ansible is 2.13.9 or later :
```
ansible-galaxy --version
```

## Upgrading Ansible
If you already have Ansible installed and want to upgrade to the newest version, use the command below:
Do this _after_ you create your Python Environment
```
python3 -m pip install --upgrade --user ansible
```

# Create Python Environment
Make sure you are in your project directory
```
pipenv install --python 3.12
pipenv install ansible
pipenv install ciscoisesdk
pipenv install paramiko
pipenv install jmespath
pipenv install passlib
pipenv shell
```
The modules for the environment shown above are
|Module|Function|
|---|---|
|python 3.12|Informs the system which version of python to use in the vitrual environment (venv)|
|ansible|Installs the most commonly used Ansible Community collections|
|ciscoisesdk|Cisco Identity Services Engine (ISE) Platform SDK for Python|
|paramiko|Python implementation of SSHv2|
|jmespath|JSON parser for Python (allows Python to read and understand JavaScript Online Notation (JSON) files)|
|passlib|Allows for `password_hash()` when creating users on linux.  macOS users may ned to use `brew install passlib`|
|pipenv shell| Activates the virtual environment|

# Install Ansible Collections
Ansible Galaxy provides pre-packaged units of work known to Ansible as roles and collections.
Content from roles and collections can be referenced in Ansible playbooks and immediately put to work. You'll find content for provisioning infrastructure, deploying applications, and all the tasks you do everyday.

Use Ansible Galaxy to install the Ansible collections:

Show the list of installed collections:
```
ansible-galaxy collection list
```

I've added the full commands in the code blocks so you can simply copy/paste them into your terminal application.

## These are the basic Ansible Collections that I install
Install the following **BASE** collections
```
ansible-galaxy collection install cisco.ise
ansible-galaxy collection install cisco.ios
ansible-galaxy collection install ansible.netcommon
ansible-galaxy collection install community.general
ansible-galaxy collection install community.aws
```
> 💡 **Note:** Add the `--force` option for rebuilding or reinstalling to overwrite existing data

## That's it!  You're ready to start!

You can keep reading if you'd like to install more Collections
* * *
* * *
# Virtual Platforms
I have added the SDKs and Ansible Collections for all the virtual platforms supported by ISE
## Cloud Providers
Install the following common collection for Cloud applications
```
ansible-galaxy collection install cloud.common
```

### AWS Collections
Install the SDK and Python Packages for AWS
```
pipenv install boto3
pipenv install botocore
```
|Module|Function|
|---|---|
|boto3| Boto3 is the Amazon Web Services (AWS) Software Development Kit (SDK) for Python|
|botocore|A low-level interface to a growing number of Amazon Web Services. The botocore package is the foundation for boto3|

Install the Ansible Collections
```
ansible-galaxy collection install amazon.aws
ansible-galaxy collection install community.aws
```

### Microsoft Azure Cloud Collections
Install the SDK for Azure Cloud
```
pipenv install ansible[azure] 
```

Install the Ansible Collections
```
ansible-galaxy collection install azure.azcollection
pip3 install -r ~/.ansible/collections/ansible_collections/azure/azcollection/requirements.txt
ansible-galaxy collection install community.azure
```

### Google Cloud Collections
Install the Ansible Collections
```
ansible-galaxy collection install google.cloud
ansible-galaxy collection install community.google
```

### Oracle Cloud Infrastructure (OCI) Collection
https://github.com/oracle/oci-ansible-collection
https://github.com/oracle/oci-ansible-collection/blob/master/InstallationGuide.md
https://github.com/oracle/oci-ansible-collection/tree/master/samples

Install the OCI python SDK
```
pipenv install oci
```

Install the Ansible Collection
```
curl -L https://raw.githubusercontent.com/oracle/oci-ansible-collection/master/scripts/install.sh | bash -s -- --verbose
ansible-galaxy collection install -f oracle.oci
```

## On Premise Hypervisors

### VMware Collections
Install the SDK for VMware
```
pipenv install pyvmomi
```

Install the Ansible Collections
```
ansible-galaxy collection install vmware.vmware_rest
ansible-galaxy collection install community.vmware
```

### Linux KVM (QEMU/KVM) Collection
Install the SDK for QEMU
```
pipenv install libvirt
```

Install the Ansible Collection
```
ansible-galaxy collection install community.libvirt
```

### Microsoft Hyper-V Collection 

```
pipenv install pywinrm
```

(https://github.com/glenndehaan/ansible-win_hyperv_guest)
```
win_hyperv_guest
```

### Nutanix
You have to compile and install the collection for Nutanix (https://github.com/nutanix/nutanix.ansible).  The collection is referred to as `nutanix.ncp`

Here are the steps to install the collection

1. Clone the GitHub repository to a local directory
```
git clone https://github.com/nutanix/nutanix.ansible.git
```

2. `cd` into the new directory
```
cd nutanix.ansible
```

3. Git checkout release version
```
git checkout <release_version> -b <release_version>
```

4. Build the collection
```
ansible-galaxy collection build
```

5. Install the collection
```
ansible-galaxy collection install nutanix-ncp-<version>.tar.gz
```

