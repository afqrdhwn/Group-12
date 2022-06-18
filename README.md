# Tutorial

## Group Members

1. Mohd Afiq Ridhwan bin Rosli (2014161)
2. Amir bin Zaid (2010829)
3. Abu Zharr Luqman bin Abdul Aziz (2011733)

## Introduction
Docker is an open source containerization platform. It allows developers to package applications into containers—standardized executable components that combine application source code with the operating system (OS) libraries and dependencies needed to run that code in any environment. Containers simplify the delivery of distributed applications and are gaining popularity as organizations move to cloud-native development and hybrid multicloud environments. Docker is essentially a toolkit that allows developers to build, deploy, run, update, and stop containers using simple commands and labor-saving automation through a single API.

Now people might go thinking that Docker is the same as virtual machines such as Oracle Virtual Machine. There is a huge difference between Docker and other virtual machines. Virtual machines create a sub-machine inside an already existing machine and the sub-machines are provided their owh HDD space, memory and processing powers which are obtained from the base machine. There, developers can create, explore and experiment with their applications without affecting the base machine's system. Docker on the other hand, create components which are provided resources such as libraries which allows developers to do the exact same process they do on virtual machines.

##  Installation Steps and Procedures (with WSL 2 backend)
__Step 1__  - Go to the website https://docs.docker.com/desktop/windows/install/ and download the Docker Desktop Installer file.
           
           Note that your computer must fulfill the following system requirements for it to be able to run Docker:
              1.  Windows 11 64-bit: Home or Pro version 21H2 or higher, or Enterprise or Education version 21H2 or higher OR
                  Windows 10 64-bit: Home or Pro 21H1 (build 19043) or higher, or Enterprise or Education 20H2 (build 19042) or higher
              2.  Enable the WSL 2 feature on Windows
              3.  Download and install the Linux kernel update package
              
__Step 2__  - After the download has been completed, run the Docker Desktop Installer.exe file.
__Step 3__  - Select the 'Use WSL 2 instead of Hyper V' option on the Configuration page when prompted.
__Step 4__  - Follow the instructions on the installation wizard to authorize the installer and proceed with the install.
__Step 5__  - Close the installation wizard when the installation is successful.
__Step 6__  - Open the Docker Desktop installed and complete the installation of WSL 2 backend (or update if needed)
__Step 7__  - Restart your computer and Docker is ready to go! 

## Code and Commands



