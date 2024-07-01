To create a new repository for your Quarkus project, you can follow these general steps. This example assumes you're using GitHub, but similar steps apply to other repository hosting services like GitLab or Bitbucket.

### Step 1: Create a New Repository on GitHub
1. **Log in to GitHub.**
2. **Click on your profile icon** in the top right corner and select **Your repositories**.
3. **Click the "New" button** to create a new repository.
4. **Fill in the repository details:**
   - **Repository name**: Give your repository a name.
   - **Description**: (Optional) Provide a brief description of your repository.
   - **Public or Private**: Choose whether you want your repository to be public or private.
   - **Initialize this repository with:** You can add a README file, .gitignore for Quarkus, and choose a license.

5. **Click "Create repository".**

### Step 2: Clone the Repository Locally
After creating the repository, you need to clone it to your local machine:

```sh
git clone https://github.com/your-username/your-quarkus-repo.git
cd your-quarkus-repo
```

### Step 3: Set Up Your Quarkus Project
If you don't already have a Quarkus project, you can create one using the Quarkus CLI or Maven:

#### Using Quarkus CLI:
1. **Install Quarkus CLI** if you haven't already:
   ```sh
   curl -Ls https://sh.quarkus.io/install.sh | bash
   ```

2. **Create a new Quarkus project:**
   ```sh
   quarkus create app org.acme:quarkus-quickstart:1.0.0-SNAPSHOT
   ```

#### Using Maven:
1. **Generate a new Quarkus project using Maven:**
   ```sh
   mvn io.quarkus:quarkus-maven-plugin:2.0.0.Final:create \
       -DprojectGroupId=org.acme \
       -DprojectArtifactId=quarkus-quickstart \
       -DclassName="org.acme.quickstart.GreetingResource" \
       -Dpath="/hello"
   ```

### Step 4: Add Your Project to the Repository
Move your Quarkus project files into your cloned repository directory, or if you generated the project inside the repo directory, just proceed with the following steps:

1. **Add the files to the repository:**
   ```sh
   git add .
   ```

2. **Commit the changes:**
   ```sh
   git commit -m "Initial commit with Quarkus project"
   ```

3. **Push the changes to GitHub:**
   ```sh
   git push origin main
   ```

### Step 5: Update Your CI/CD Pipeline
If you are integrating this with a CI/CD pipeline (as it appears you are with Azure DevOps), update your pipeline configuration accordingly to point to your new repository and configure the necessary build steps for Quarkus.

### Example Azure DevOps Pipeline for Quarkus
Here is a basic example of what your `azure-pipelines.yml` might look like for a Quarkus project:

```yaml
trigger:
  branches:
    include:
      - develop
      - release/*
      - main

pool:
  vmImage: 'ubuntu-latest'

variables:
  JAVA_HOME: '/usr/lib/jvm/adoptopenjdk-11-hotspot'

steps:
- task: Maven@3
  inputs:
    mavenPomFile: 'pom.xml'
    mavenOptions: '-Xmx1024m'
    javaHomeOption: 'JDKVersion'
    jdkVersionOption: '1.11'
    jdkArchitectureOption: 'x64'
    publishJUnitResults: true
    testResultsFiles: '**/target/surefire-reports/TEST-*.xml'
    goals: 'clean install'

- task: Docker@2
  inputs:
    command: build
    repository: 'your-docker-repo/your-quarkus-app'
    dockerfile: '**/src/main/docker/Dockerfile.jvm'
    tags: '$(Build.BuildId)'

- task: Docker@2
  inputs:
    command: push
    repository: 'your-docker-repo/your-quarkus-app'
    tags: '$(Build.BuildId)'
```

Adapt this configuration to fit your specific requirements and repository structure. This setup will build your Quarkus project and create a Docker image from it, which can then be pushed to your Docker repository.
