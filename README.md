# docker-msre
This repo is created for the purpose of creating a docker conatiner which includes not only support for OpenMC w DAGMC/MOAB, embree, and double_down libraries, but also a Jupyter notebook server. The "reason d'etre" for this is to run a virtual version of The Molten Salt Reactor experiment (MSRE). The experiment itself was performed physically in the '60s at Oak Ridge National Lab (ORNL), Tennessee.

# Getting started:
1. Install the docker engine on your system (for windows and MacOS: docker-desktop, for Linux: docker server)
  Instructions for how to do this may be found on the Docker website at: [Docker installation](https://docs.docker.com/engine/install/)
2. Run the msre docker container.
    - Linux:
        1. Open a terminal, navigate to a directory where you want to run.
        2. Download the msre-docker runscript, and run it:
        ```{bash tidy=false}
        wget https://raw.githubusercontent.com/openmsr/docker-msre/main/run_docker.sh
        chmod u+x run_docker.sh
        ./run_docker.sh
        ```
        The script contains a call to ```docker run``` with some options preset. Among other things it sets up a subdirectory called notebooks which is shared between the conatiner and the host so that you can keep data between runs.
        Feel free to inspect the runscript if you prefer to run your docker manually. If you'd prefer for instance to run commands in the docker from a shell
        you may do so by adding the option ```--entrypoint /bin/bash``` to the docker run command.
        3. If you used the run-script "as is" you should now be able to open a browser and point it to "https://127.0.0.1:8888" and be treated with a login page to Jupyter.
        Please enter "docker" in the password box, which should provide you with the base Jupter Lab screen.
        4. In the example_notebooks folder open the MSRE.ipynb file. You are now ready to run!
      
      ## Troubleshooting:
        - If you get an error message saying: "docker: Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?." that likely means that you need to start the docker engine. This can be done using the command:  
        ```sudo dockerd```  
        - If you get an error similar to: "Got permission denied while trying to connect to the Docker daemon socket...", it is likely that your user needs to be added to the "docker" group. To check which groups your user belongs to you may use the groups command. To add your user to the docker group you may use:  
        ```sudo usermod -aG docker <username>``` where <username> is your username. 
        
  - Windows:
    There are two options for running the docker on a windows system:
    1. Install the docker-desktop application.
    2. Install Windows Subsystem for Linux (WSL) and run the docker from the command-line there.
    N.b. In fact the docker-desktop application also relies on WSL. 
    WSL is a native windows system that enables users to run anyh and all Linux applications natively on Windows 10 and 11, including parallelization and even access to acceleration through GPUs.
    Please note that the process may require updates to Windows to be installed and also rebooting your system. Furthermore, it may also require you to edit settings in the BIOS to enable virtualization on your system.  
    If you chose the former route, you may proceed by opening docker-desktop application and follow the steps outlined there to get started. To run this particular docker you should open a command prompt and issue the follwing command: ```docker run -e JUPYTER_ENABLE_LAB=yes -e JUPYTER_TOKEN=docker -v notebooks:/home/usr/notebooks copenhagenatomics/msre:0.1.0```. This is actually what the last line of the run_script does.  
    If you chose the latter route, we have to first install a Linux kernel in WSL. Open a command prompt and run the command ```wsl --install -distribution debian``` (or shorter ```wsl -d debian```)
    Once this is done we start wsl, you may proceed to get the run-script using wget:
    ```wget --no-check-certificate https://raw.githubusercontent.com/openmsre/docker-msre/main/run_docker.sh```
    
