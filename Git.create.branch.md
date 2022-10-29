 ##### Create a branch from the master branch. 
 
 > Nautilus developers are actively working on one of the project repositories, /usr/src/kodekloudrepos/ecommerce. 
 > They recently decided to implement some new features in the application, and they want to maintain those new changes in a separate branch. 
 > Below are the requirements that have been shared with the DevOps team:

 > On Storage server in Stratos DC create a new branch xfusioncorp_ecommerce from master branch in /usr/src/kodekloudrepos/ecommerce git repo.

 . Please do not try to make any changes in code.
 
 ```
 1. Switch to the storage serverby ssh into it - ssh usrname@hostname 
 
 2. Next change directory to the working directory of the team -> cd /usr/src/kodekloudrepos/ecommerce. 
 
 3. Check all the branches -> git branches -a
 
 4. Check the git status. 
 
 5. swutchto the master branch -> sudo git checkout master
 
 6. Create the xfusioncorp brnahc -> sudo git checkout -b xfusioncorp_ecommerce
 
 7. confirm that xfusioncorp_ecommerce wass created -> git branch -a 
 
 ```
