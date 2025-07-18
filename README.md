## Freestyle project on Jenkins
### what is Jenkins

In Jenkins, a job is a unit of work or a task that can be executed by the Jenkins automation server.

A Jenkins job represents a specific task or set of tasks that needs to be performed as part of a build or deployment process. Jobs in Jenkins are created to automate the execution of various steps such as compiling code, running tests, packaging applications, and deploying them to servers. Each Jenkins job is configured with a series of build steps, post-build actions, and other settings that define how the job should be executed.

The project described in the image is about **setting up and automating a Jenkins Freestyle Project** with integration to **GitHub**. Here's a summary of the key steps:

---

### 🔧 **Project Overview**

* **Goal:** Automate a build process using Jenkins whenever code changes are pushed to a GitHub repository.

---

### ✅ **Steps Involved**

1. **Creating a Freestyle Project:**

   * Create a new Jenkins job called `my-first-job` using the Freestyle project option.

2. **Connecting Jenkins to GitHub (Source Code Management):**

   * Create a GitHub repository (`jenkins-scm`).
   * Configure Jenkins to use this repository and make sure the branch is set to `main`.
   * Save and trigger the initial build manually to verify the connection.

3. **Configuring a Build Trigger:**

   * Set up Jenkins to automatically trigger builds using GitHub webhooks.
   * Enable the "Build when a change is pushed to GitHub" trigger.
   * Create a GitHub webhook using the Jenkins server's IP and port.

---

### 🛠 **Outcome**

After setup, every code change (e.g., README edits) pushed to the GitHub repository will automatically trigger a Jenkins build via the webhook—no manual "Build Now" required.

### Solution to the Project
- Reference [installation-guide](https://github.com/Heebrah/intro-to-jekins) and follow the download guideline.
1. Go to Jenkins dashboard and click **new item**
![caption](/img/1.dashboard.jpg)

2. Name my project **my-first-project** and select **Freestyle project** ![caption](/img/2.free-style-project.jpg)

3. I create a new repository name **jenkins-scm** and add a README.md file
![caption](/img/3.repository-created.jpg)

4. Now i connect the github by adding the github url into the jenkins project under **Source Code Management** choose **Git** then paste the url into **Repository url**

![caption](/img/10.add-git.jpg)

5. scroll down to see **Branch Specifier** and choose main because we are on main branch
```
*/main
```
![caption](/img/11.main-branch.jpg)

6. Then go to triger and check
**GitHub hook trigger for GITScm polling**
![caption](/img/12.trigger.jpg)

7. Now is to add the jenkins public ip address into the webhook on github so that any changes made from github will trigger a change in build in the jenkins project build

For my project i'm using an ngrok to serve as my public ip address for jenkins

to install ngrok use the command
```
sudo snap install ngrok
```
![caption](/img/24.ngrok-installation.jpg)


8. create a ngrok account using this 
```
https://dashboard.ngrok.com
```
and move to **Your Authtoken** to copy the token
![caption](/img/27.autentication.jpg)


9. authenticate the token on terminal
```
ngrok config add-authtoken $Your_Authotoken
```
*$Your_Authtoken* is the token you copied from ngrok dashboard

![caption](/img/28.authenticate-ngrok.jpg)

10. If the register for a paid version of ngrok then you can follow this step below
**Reserve a Static Domain**

1. Go to:
   👉 [https://dashboard.ngrok.com/cloud-edge/domains](https://dashboard.ngrok.com/cloud-edge/domains)

2. Click **“Reserve a Domain”**

3. In the **subdomain field**, type something unique like:

   ```
   jenkins-ibrahim
   ```

   Your full domain will become:

   ```
   jenkins-ibrahim.ngrok.io
   ```

4. Click **Reserve**

---

 **Start ngrok with Your Reserved Domain**

Now that the subdomain is reserved, run:

```bash
ngrok http --domain=jenkins-ibrahim.ngrok.io 8080
```
![caption](/img/26.ngrok-webpage.jpg)

11. using free version we can run ngrok with the command

```
ngrok http 8080
```
like we know jenkins runs on port 8080 of our local network. 
![caption](/img/25.run-grok-on-8080.jpg)

12. we can get our public ip address equivalent to localhost:8080 as something like https://.....ngrok.free.app.
N.B this changes as we reload so we will need to be changing the jenkins ip address

![caption](/img/23.ngrok-http-8080.jpg)

13. After we have gotten our public ip address we will go to the jenkins dashboard and click **manage jenkins**
![caption](/img/20.manage-jenkins.jpg)

14. then go to **system**
![caption](/img/21.system-jenkins.jpg)

15. and look for **Jenkins Url** and paste the public ip address there
![caption](/img/22.public-ip-address.jpg)

16. Now we can move to the github repository and go to **setting** under the project repo and go to **webhook** 
![caption](/img/13.webhook-github.jpg)

17. click on **Add webhook**
![caption](/img/29.add-webhook.jpg)

18. input your public ip address into the payload and add /github-webhook/ so you will have something like https://......ngrok-free.app/github-webhook/
content type should be **json**
and select **just the push event**
![caption](/img/30.added-webhook.jpg)

19. Now i can go into my README.md file to make changes into it and go to the webhook to see if it push it into my jenkins. if it's successful it will mark a green stripe
![caption](/img/14.successful-github-update.jpg)

20. to see this on my jenkins 
![caption](/img/31.going-to-build.jpg)
then click the latest build

21. click details
![caption](/img/15.update-success.jpg)

22. i can see the commit message i used to update my README.md
![caption](/img/16.updated-changes-jenkins.jpg)

Finished. Thank You.





