# Purpose

This article goes over how to integrate the blog repository with Azure Data Studio

# Resources

R1: To enable Git with Azure Data Studio: https://docs.microsoft.com/en-us/sql/azure-data-studio/source-control?view=sql-server-ver16#git-support-in-azure-data-studio
R2:  Azure Data Studio GIT Integration: https://www.youtube.com/watch?v=EmSrQCDsMv4
R3: Jekyll Installation on Windows: https://kencenerelli.wordpress.com/2017/03/08/installing-jekyll-on-windows/
R4: Jekyll installation on Windows (This one goes over msys related error) - https://gist.github.com/arthurattwell/281a5e1888ffd89b08b4861a2e3c1b35 

# Steps to integrate Azure Data Studio with Git Repo

1. Install Azure Data Studio if not already available on your Windows machine.
2. Install Git for Windows (Azure Data Studio ships with a Git source control manager (SCM), but you still need to install Git (version 2.0.0 or later) before these features are available.) 
Note: Reference https://docs.microsoft.com/en-us/sql/azure-data-studio/source-control?view=sql-server-ver16 for the latest version of Git installation
3. If the installation from step 2 is complete, you will now see that Git integration in source control becomes available. You can clone the Git repository from your URL to the local Windows machine at this time.  
Note: If there are any pending updates available , please update Azure Data studio. When updates are pending, the Git integration may not fully go through. 
5. Once cloning is successful, ensure that Jekyll is installed on your Windows machine. Please refer to the resource R3 on the resources section for Jekyll installation walkthrough. Please note that you may get msys related errors with Jekyll installation. If you run into that issue, the following additional commands to be executed to correct the issue: (Reference R3 from resources section)
* Install MSYS2. This provides extra tools required for Jekyll's native extensions. To do this, run choco install msys2. (More details here.) Again, close the Command  
  Prompt and open it again as an administrator.
* Run the RIDK installer. Still more tools for native extensions. enter ridk install and at the prompts choose the default option to run options 1, 2 and 3 at once. 
* Re-run the command gem install jekyll
6. Utilize the video walkthrough listed in R2 under resources to complete the Azure Data Studio Git blog integration!

