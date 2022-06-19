# Tutorial to Install Docker for Apache, MySQL and PHPMYADMIN on Windows OS
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
__Step 1__  - Open your command prompt

![image](https://user-images.githubusercontent.com/103871912/174485459-d9575ba4-a492-42c8-957d-818c210d441f.png)

__Step 2__  - Create a folder for your project, type in: __mkdir <-poject name->__. Replace __<-project name->__ with whatever name you want for your project.

![image](https://user-images.githubusercontent.com/103871912/174485531-2f189333-4d00-4772-ae85-2c1d6f69b3db.png)

__Step 3__  - Now, change the directory inside the command prompt to your project, type in: __cd <-project name->__.

![image](https://user-images.githubusercontent.com/103871912/174485546-46861b10-0ba6-4da0-bff7-dd9264e22b6e.png)

__Step 4__  - It should show something like this: __C:\Users\user\<-project name->__. Since my project's name is project it will show project.

![image](https://user-images.githubusercontent.com/103871912/174485556-6d010499-a7c7-4233-a808-fcc24ed9ccb3.png)

__Step 5__  - From here, type in: __code .__. This will open Visual Studio Code to edit your project's folder. If you still do not have Visual Studio Code, I recommend installing it as it is very helpful for your coding endeavors in the future.

![image](https://user-images.githubusercontent.com/103871912/174485719-bc434ed3-4436-49b7-8e2e-8ee28b767537.png)

__Step 6__  - In your folder, you need to create a .yml file which contains the information of the services you need for your project(apache, mysql and myphpadmin). Type: __mkdir docker-compose.yml__ into your command prompt. You can name the file anything you want but in the future you need to remember the name. The content of your .yml fileshould be: 

                      version: '3.8'
                      services:
                        php-apache-environment:
                          container_name: php-apache
                          image: php:8.0-apache
                          volumes:
                          - ./php/src:/var/www/html/
                          ports:
                          - 8000
                          
This is the initial configuration for your localhost, from which you can view the project you are building.
__Step 7__  - Go back to the command prompt and create another folder called __php__ and inside it another folder called ___src__ . The command for it is __mkdir php__, __cd php__ and __mkdir src__. In the src folder crete another folder called index.php. This index file is important as you will be editing the front end of your project here. So for Step 7, the directory for the folder php should be: __/php__, src: __/php/src__ and index.php: __/php/src/index.php__.

__Step 8__  - Add some lines of code in the index.php file and run your localhost server. Try adding:

                      <?php
                         echo "Hello World!";
                      ?>
                     
To run your localhost type in __docker-compose up__ and after a it finishes loading everything in the command prompt, go to your favorite browser and type in: __localhost:8000__. You might have noticed that the port is the same as the code we put inside the .yml file and this is because most localhosts of any machine run on port 8000. In your screen, there should be a Hello World! displayed. You can alter the index.php file to develop your project after we have finished setting up all the environment needed. You can check in your Docker -> Containers and see that your project's first container is running.

__Step 9__  - Here we are gonna add another environment for your propject which is MYSQL. To do this, add this MYSQL configuration inside the .yml file:

                      version: '3.8'
                      services:
                        php-apache-environment:
                                 container_name: php-apache
                                 build:
                                   context: ./php
                                   dockerfile: Dockerfile
                                 depends_on:
                                   - db
                                 volumes:
                                   - ./php/src:/var/www/html/
                                 ports:
                                   - 8000
                        db:
                                 container_name: db
                                 image: mysql
                                 restart: always
                                 environment:
                                   MYSQL_ROOT_PASSWORD: MYSQL_ROOT_PASSWORD
                                   MYSQL_DATABASE: MYSQL_DATABASE
                                   MYSQL_USER: MYSQL_USER
                                   MYSQL_PASSWORD: MYSQL_PASSWORD
                                 ports:
                                   - "9906:3306"
                                 
Note: you need to overwrite the previous code. Then, head on to the /php folder and add a Dockerfile. Just type in: __mkdir Dockerfile__ after you get into /php and walla! A Dockerfile is a file which can only be recognize by Docker and it does not need any file type written. In the Dockerfile type:

                      FROM php:8.0-apache
                      RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli
                      RUN apt-get update && apt-get upgrade -y
                      
In your index.php, fill in the following code (replace the existing ones):  

                      <?php

                        $host = 'db';

                        // database username
                        $user = 'MYSQL_USER';

                        // database user password
                        $pass = 'MYSQL_PASSWORD';

                        // check the MySQL connection status
                        $conn = new mysqli($host, $user, $pass);
                        if ($conn->connect_error) {
                                 die("Connection failed: " . $conn->connect_error);
                        } else {
                                 echo "Connected to MySQL server successfully!";
                        }
                      ?>
                      
Now to see what changes in your project, you need to restart your project by typing: __docker-compose down__ and __docker-compose up__ again. Check your Docker and you should see two sub-containers running in your project's container. Also, you can refresh your localhost:8000 and see whether the connection to your MYSQL database server is successful or not. If its successful it should display "Connected to MYSQL server successfully!".

__Step 10__ This step will be the final step, which is adding phpmyadmin to your project. First, add this code under the existing code in your .yml file:

                      phpmyadmin:
                        image: phpmyadmin/phpmyadmin
                        ports:
                           - '8080:80'
                        restart: always
                        environment:
                           PMA_HOST: db
                        depends_on:
                           - db

Restart you project (__docker-compose down__ and __docker-compose up__) and open another tab on your browser and type in: __localhost:8080__. This is different from the previous localhost because we set up myphpadmin on port 8080 whereas MYSQL server is on 8000. It should display a login panel. To sign in, use the username: root and password: MYSQL_ROOT_PASSWORD as stated in the myphpadmin configuration. Now you are ready to develop your project using apache, MYSQL and myphpadmin. Happy Developing!
