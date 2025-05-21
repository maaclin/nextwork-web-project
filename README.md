<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a CI/CD Pipeline with AWS

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-devops-codepipeline-updated)

**Author:** Yossief Solomon  
**Email:** ysolom90@gmail.com

---

![Image](http://learn.nextwork.org/sparkling_violet_festive_wombat/uploads/aws-devops-codepipeline-updated_fbdetger)

---

## Introducing Today's Project!

In this project, I will demonstrate putting together an automated CI/CD pipeline with AWS CodePipeline. 

### Key tools and concepts

Main services I used were AWS CodeDeploy, CodeBuild, CodeArtifact and CodePipeline. The key concept of this project is the process of automating changes to our code in CI/CD pipeline and showcasing the AWS resources work in action together. 

### Project reflection

This project took me approximately 3 hours. There were alot of errors along the way which I needed to refer back to documentation to try deduce the problem but after repeating the process several times you can learn from key mistakes. 

---

## Starting a CI/CD Pipeline

AWS CodePipeline can create a workflow that automatically moves your code changes through the build and deployment stage. In our case, you'll see how a new push to your GitHub repository automtically triggers a build in CodeBuild (continuous integration) and then a deployment in CodeDeploy (continuous deployment).

CodePipeline offers different execution modes determining how the pipeline is run. I chose superseded so new changes to code overwrite any pipeline execution from previous changes to ensure we always have the latest update to our code pushed. Other options include queued, which will result in each change happening one after another and parallel which allows multiple changes at once independently. 

A service role gets created automatically during setup to give CodePipeline permission to access other AWS resources it needs to run your pipeline. 

![Image](http://learn.nextwork.org/sparkling_violet_festive_wombat/uploads/aws-devops-codepipeline-updated_gdnhtm)

---

## CI/CD Stages

The three stages I've set up in my CI/CD pipeline are the Source, Build, and Deploy stages.

The Source stage, where I connected to a GitHub repository and specified the master branch. This stage fetches the latest code changes, triggering the pipeline upon new commits.   

The Build stage, where I used AWS CodeBuild to compile and package the web application. This stage transforms the source code into deployable artifacts.   

The Deploy stage, where I configured AWS CodeDeploy to deploy the built artifacts to an EC2 instance. This stage automates the deployment process, ensuring smooth and efficient updates.

CodePipeline organizes the three stages into Source, Build and Deploy. In each stage, you can see more details on in progress actions and successful/unsucessful deployments. 

![Image](http://learn.nextwork.org/sparkling_violet_festive_wombat/uploads/aws-devops-codepipeline-updated_fbdetger)

---

## Source Stage

In the Source stage, the default branch tells CodePipeline which branch will be used when pipeline execution starts. 

The source stage is also where you enable webhook events, which is integral in a CI/CD pipeline as it what allows the process to be continuous by reacting to changes in code in real time. 

![Image](http://learn.nextwork.org/sparkling_violet_festive_wombat/uploads/aws-devops-codepipeline-updated_sergt)

---

## Build Stage

The Build stage sets up our source code to get transformed into a deployable build artifact. The input artifact for the build stage are the outputs from the previous stage that are used as inputs for the current stage.

![Image](http://learn.nextwork.org/sparkling_violet_festive_wombat/uploads/aws-devops-codepipeline-updated_j1k2l3m4)

---

## Deploy Stage

The Deploy stage is where you choose how you want to deploy your application or content. I configured to use the AWS CodeDeploy provider in our region using our build artifact within our application and deployment group. 

![Image](http://learn.nextwork.org/sparkling_violet_festive_wombat/uploads/aws-devops-codepipeline-updated_m4n5o6p7)

---

## Success!

Since my CI/CD pipeline gets triggered by changes in my repo, I tested my pipeline by adding a line to our index.jsp and pushing to github to see the results. 

The moment I pushed the code change it triggered a new execution for our pipeline. The commit message under each stage reflects the commit notes added to our github. 

Once my pipeline executed successfully, I checked my webpage to see the newly added text showing that the pipeline was successful. 

![Image](http://learn.nextwork.org/sparkling_violet_festive_wombat/uploads/aws-devops-codepipeline-updated_e1f2g3h4)

---

## Testing the Pipeline

In a project extension, I initiated a rollback on our deploy stage. Automatic rollback is important if the latest changes caused problems and you want to revert back to the latest working stage of our application. 

During the rollback, the source and build stage are kept the same as I only rolled back the deploy stage. I could verify this by viewing the deploy stage turning red and the rest staying green. 

After rollback, the live web app reverted to the old text before my changes on index.jsp. 

![Image](http://learn.nextwork.org/sparkling_violet_festive_wombat/uploads/aws-devops-codepipeline-updated_sdfgsdfgdf)

---

---
