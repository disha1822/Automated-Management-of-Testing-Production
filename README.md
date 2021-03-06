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

# Project Description :
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
 * In the **Source Code Management** we need to set our **Github Credentials** unless it will fail to merge branches.
 ![Job3_2](https://github.com/disha1822/Automated-Management-of-Testing-Production/blob/master/merge_job_2.jpeg?raw=true)
 * **Post Build Action** will perform the merge but we need to specify any build before that. In my case I have just Executed a date command in shell.
 ![Job3_3](https://github.com/disha1822/Automated-Management-of-Testing-Production/blob/master/merge_job_3.jpeg?raw=true)
 
# Testing :
Now that we have configured all the jobs in Jenkins, we can start our testing ---
## Before Feature Added
Initially our **Github master & dev1 branch** has 10 commits with the latest ocommit **test 10**.

* **Initial github master branch**

![a](https://github.com/disha1822/Automated-Management-of-Testing-Production/blob/master/initial_github_master.jpeg?raw=true)

* **Initial github dev1 branch**

![b](https://github.com/disha1822/Automated-Management-of-Testing-Production/blob/master/initial_github_dev1.jpeg?raw=true)

* **Initial Production system**

![c](https://github.com/disha1822/Automated-Management-of-Testing-Production/blob/master/initial_production_sys.jpeg?raw=true)

* **Initial Testing system**

![d](https://github.com/disha1822/Automated-Management-of-Testing-Production/blob/master/initial_testing_sys.jpeg?raw=true)

## After Feature Added
* Now developer has added one feature in **dev1 branch** and commit it in local repository. As we have created a **post-commit hook** so as soon as developer commits code is **automatically pushed in dev1 branch in Github**.
* So our job2 run and updates the Testing system.

* **Final Github dev1 branch**

![e](https://github.com/disha1822/Automated-Management-of-Testing-Production/blob/master/final_github_dev1.jpeg?raw=true)

* **Final Testing System**

![f](https://github.com/disha1822/Automated-Management-of-Testing-Production/blob/master/final_testing_sys.jpeg?raw=true)

* **Before Merging Production System**

![h](https://github.com/disha1822/Automated-Management-of-Testing-Production/blob/master/before_merge_prod_sys.jpeg?raw=true)

* Now that our testing code is running perfectly in testing environment, so the **QAT** triggers the Job3.

* **Triggerring Merging Job**

![i](https://github.com/disha1822/Automated-Management-of-Testing-Production/blob/master/trigger_merge_job.jpeg?raw=true)

* After Job3 run it has merged the **dev1 branch to master branch** and since master branch has changed so Job2 is treiggred and updated the production system.

* **After Merging Github master branch**

![g](https://github.com/disha1822/Automated-Management-of-Testing-Production/blob/master/after_merge_github_master.jpeg?raw=true)

* **After Merging Production System**
![h](https://github.com/disha1822/Automated-Management-of-Testing-Production/blob/master/after_merge_prod_sys.jpeg?raw=true)

# Future Enhancements:

Due to the limited time of the task submission and for the sake of simplicity I have used some **Trigger Options** that can be further modified ---

* Here I have used **Poll SCM** for triggerring the **Testing & Production Deployment Jobs** for which Jenkins have to keep track of Github every minute and this increases the Computation and overheads. So instead of that we can use **Github Webhook Trigger** where **Github will trigger the Jobs whenever any change occurs.**
* Also the **Merging Job is build Manually** which breaks the **Automation**. Here we can use **Remote script trigger** i.e., the **QAT will trigger the Job with some remote script in their system**.

# Lastly, I will like to thank Vimal Sir from the bottom of my heart. Just in 8 Days of training we have learnt so much only for him.
