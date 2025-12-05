[[_TOC_]]

# Ansible Fundamentals Training

In this training course individuals will learn more about the fundamentals of Ansible in Chevron.

Topics include:

- Automation
- Infrastructure as Code
- Introduction to YAML
- Ansible Roles in Chevron
- Coding tools
- IaaS overview and setup

## How to sign-up for this self-service training? (5 minutes)

Go to the [signup link](https://go.chevron.com/SelfServiceTrainingSignup) and choose which class you'd like to join (select **SST-Ansible-Fundamentals**). You can change the the duration (1-21 days) for how long to be enrolled in the class. you will be notified via teams that the course is ready for you. You will have your own environment and resource group to use for the duration of this training.

Here's an example notification that you will get in MS Teams when your newly created repository and environment has been created.

- Take note of the specific details assigned to you such as the **environment** and **resource group**.
- Click the **Open My Repo** button to navigate to your repository.

  ![sst-aks-signup-notification](/.attachments/SST-Notification.png)

For this training there is a [slide deck](http://go.chevron.com/ansibletraining) that individuals can go through as well as [instructional videos](https://go.chevron.com/ansiblefundamentalsvideo) covering the slide deck in detail.

## Exercises

---

<details><summary><font size="+2"><b>Exercise 0: Creating New Pipeline, Adding Pipeline Variable, and Running Pipeline Updater (15 minutes)</b></font></summary>

---

### Exercise 0: Creating New Pipeline, Adding Pipeline Variable, and Running Pipeline Updater (15 minutes)

In this exercise, you will be using your personal repository that was created in the pre-work section. You will create a new branch in Azure DevOps (ADO) and run the Update Pipeline to prepare for subsequent exercises.

Please follow these steps:

1. Go to [ITC-ITSD-ITFPAPESSelfServiceTraining](https://dev.azure.com/chevron/_git/ITC-ITSD-ITFPAPESSelfServiceTraining). Under **Repositories**, search and select the repository that is prefixed with your **email** (ex: **myemail-SST-Ansible-Fundamentals**).
2. On your own repository in ADO, create a new branch from **master**. This will be your working branch.
3. On VScode on our local machine, clone the repository to work offline, or edit files directly in the ADO Web UI.

   > Tips:
   >
   > - For multiple file modifications, cloning and using an editor like VSCode or Visual Studio is recommended for a single-commit workflow.
   > - Access the web version of VSCode by pressing the '.' (dot) key in the repository view or visit [https://vscode.dev/](https://vscode.dev/) and open your repository.

4. Open the [azure-pipelines.yml](/azure-pipelines.yml) file and update the **deployEnvironment** parameter on line 17 to your assigned environment number from registration (e.g., **default: dev15**).
5. Stage and commit your changes. If working locally, push them to your ADO remote repository.
6. In a new browser tab, visit the <a href="https://dev.azure.com/chevron/ITC-ITSD-ITFPAPESSelfServiceTraining/_build" target="_blank">Pipelines</a> section.
7. Click '**New Pipeline**'.
8. Choose '**Azure Repos Git**' and select your repository (e.g., **myemail-SST-Ansible-Fundamentals**).
9. On the **Configure your pipeline**, choose **Existing Azure Pipelines YAML file**.
10. On the pop-up window for **Select an existing YAML file**, set the branch to master and set the path to **/azure-pipeline.yml**.
11. On **Review your pipeline YAML** window, click the dropdown on the right of **Run** button and click **Save**. You're new pipeline is created!
12. Run the pipeline updater to attach required variable groups.

    - Choose '**Run pipeline**'.
    - Select your branch under '**Branch/tag**'.
    - Enable '**Update Pipeline**' and click '**Run**' to update your pipeline with necessary resources like variable groups, environments, and service connections.

      The **Update Pipeline** could take more than 10 minutes to complete. The duration could extend further if there is a high number of participants involved.

> Additional reading materials:
>
> - [CDAS - Source Control Management (SCM)](https://cdas.azure.chevron.com/ITE-APES/Software-Engineering/Source-Control.html)
> - [CDAS - Pipeline Updater](https://cdas.azure.chevron.com/CVX-DevOps.wiki/ADO-Pipeline/Components/Pipeline-Updater.html)

</details>

---

<details><summary><font size="+2"><b>Exercise 1 - Setup Jupyter Notebook learning environment (1 hour)</b></font></summary>

---

### Exercise 1A: Modify and Deploy Jupyter Notebook learning environment (30 min)

<details>
   <summary><font size="+1"><b>Initial lab setup</b></font></summary>

---

You must complete **Exercise 0** before proceeding with this exercise.

The ansible warnings being prevented:

```
[WARNING]: Unable to parse /etc/ansible/hosts as an inventory source
[WARNING]: No inventory was parsed, only implicit localhost is available
[WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does not match 'all'
```

##### **Deploy Jupyter Environment**

1. Return to the pipeline you created in **Exercise 0**.
2. Click on the **Run** button to open the run options.
3. Select the branch you created in **Exercise 0**.
4. Click on the **Run** button to start the pipeline.
5. Once the pipeline is running it will take around 20 - 30 minutes to complete. You can monitor the progress of the pipeline by clicking on the Deploy Jupyter Stage.
6. Once the pipeline has completed, you will need to get the url for the jupyter notebook environment. You can find this in one of two ways:
    - Click on the **Deploy Jupyter** stage and then find the task named `Output IP address at end of log` and click the link it outputs
    ![Output IP address at end of log](/.attachments/ip-in-logs.png)
    - Navigate to your environment in the azure portal
      - It will be named `apelrn-l019-<your-environment>-<datecode-when-created>`. You can find this by searching for `apelrn-l019-<your-environment>` in the search bar at the top of the portal. (If its not found make sure that you are not filtering out the l019 subscription)
      - Once you are in your resource group there should be a virtual machine named apelrn-(d/t)<your-environment>app00
      - Click on the vm and locate the private IP address. This is the IP address you will use to access the jupyter notebook environment.




    The pipeline will deploy a Jupyter Notebook environment in your assigned Azure environment. This environment will be used for the rest of the training.

    The ip address to in the url bar should look like:

    `http://<ip-address>:8080`
    ![IP in url](/.attachments/ip-in-url.png)

Once there you will see the following screen:

![Jupyter Start Page](/.attachments/jupyter-start.png)


Double click `1 - Inro to Ansible.ipynb` to open the first notebook. Follow the instructions in the notebook to complete the exercise, and then proceed through the rest of the notebooks in order.

</details>

---


## What you can do next?

- Enroll to other Self-Service Trainings
- Explore the ansible roles that are available in Chevron at the [Ansible Roles Project](https://dev.azure.com/chevron/AnsibleRoles)
- Explore the other resources at the [CVX Ansible Roles User Guide](https://dev.azure.com/chevron/AnsibleRoles/_wiki/wikis/AnsibleRoles.wiki/110748/Ansible-Roles-User-Guide)


## Troubleshooting

If the pipeline updater fails due to not being able to find a keyvault matching your dev environment, please wait an hour or so and attempt again. This may occur within the first hour or two after your environment is created.

If the pipeline fails to run due to permission errors on a keyvault:

- Run the pipeline updater again by selecting the **Update Pipeline** option.

---

Content Owner: Dan Argueza (aargueza@chevron.com)
