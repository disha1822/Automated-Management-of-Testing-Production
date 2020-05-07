# Automated Management of Testing Production Systems 

# Home Task Given by Mr. Vimal Daga Sir Under DevOps Assembly Lines Training

# Project Overview :
In this project I have created a **Continuous Integration & Continuous Deployment Pipeline** for the deployment of a webserver. We have 4 systems ---
 * 1. Devloper's System:
    Devloper has a local repository maintaining 2 branches **master** and **dev1** (feature branch).
 * 2. SCM System:
    In our case Github is the SCM System that maintains the same structure as of the Developr.
 * 3. Production System:
    In this system we deploy the well tested code in the **master** branch.
 * 4. Testing System:
    Here we deploy the code in the **dev1** branch for **feature testing**.
# Required Softwares :
  * Git
  * Jenkins
  * Docker

# Description :
I have designed **three** jobs in **Jenkins** to achieve this CI/CD Pipeline of testing and production deployment ---
## Job1 (Deployment in Testing Environment) :
 * This job will go to the github repository specified in SCM Section and copy the code in the **dev1** to one local directory of testinf system and then deploy it to a **Docker container** monting the directory.
 * We triggered the job by **Poll SCM** so it will check the dev1 branch every minute and if aby change occur it will run the job.
 ![Job1_1]()
