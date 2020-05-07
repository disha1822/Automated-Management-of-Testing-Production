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
 * This job will go to the github repository specified in SCM Section and copy the code in the **dev1 branch** to one local directory of testing system and then deploy it to a **Docker container** mounting that directory.
 * We triggered the job by **Poll SCM** so it will check the dev1 branch every minute and if any change occur it will run the job.
 ![Job1_1](https://github.com/disha1822/Automated-Management-of-Testing-Production/blob/master/testing_job_1.jpeg?raw=true)
 ![Job1_2](https://github.com/disha1822/Automated-Management-of-Testing-Production/blob/master/testing_job_2.jpeg?raw=true)
 
 ## Job2 (Deployment in Production Environment) :
 * This job will go to the github repository specified in SCM Section and copy the code in the **master branch** to one local directory of production system and then deploy it to a **Docker container** mounting that directory. Here we also need to expose the port 80of the container as clients are connected to it.
 * We triggered the job by **Poll SCM** so it will check the master branch every minute and if any change occur it will run the job.
 ![Job2_1](https://github.com/disha1822/Automated-Management-of-Testing-Production/blob/master/production_job_1.jpeg?raw=true)
 ![Job2_2](https://github.com/disha1822/Automated-Management-of-Testing-Production/blob/master/production_job_2.jpeg?raw=true)
 
 ## Job3 (Merging branches) :
 * This job will merge the **dev1 branch** with the **master branch** .
 * Whenever the **Quality Assurance Team** makes sure that the features added to the server is working fine in **testing Environment** 
 they will trigger **Job3** and this job will merge the branches.
 * As a result changes occur in the **master branch** which will in turn trigger **Job2** that deploys the **new well tested features**
 of master to the **Production System**.
 ![Job3_1](https://github.com/disha1822/Automated-Management-of-Testing-Production/blob/master/merge_job_1.jpeg?raw=true)
 ![Job3_2](https://github.com/disha1822/Automated-Management-of-Testing-Production/blob/master/merge_job_2.jpeg?raw=true)
 ![Job3_3](https://github.com/disha1822/Automated-Management-of-Testing-Production/blob/master/merge_job_3.jpeg?raw=true)
 
