![Video Tutorials](https://www.youtube.com/playlist?list=PLGTmxtJmro0qkaUSx4dXC-YODw9jCJ_Uu)

# How to Run a Database Server with a GitHub Actions Workflow
## 1. Create the Workflow File

In the root directory of your GitHub repository, create a folder named .github/.
Inside .github/, create a folder named workflows/.
Inside workflows/, create a new file with the extension .yml or .yaml. For example: explore_actions.yml.

## 2. Complete YAML File Content

The code you provided is only the definition of a Job. For it to be a complete and executable Workflow, it needs a name and a trigger (on).
Copy and paste the following content into the explore_actions.yml file:

name: Explore GitHub Variables

on:
  # The workflow will run when there is a push (commit) or a pull request
  push:
    branches: [ "main", "master" ]
  pull_request:
    branches: [ "main", "master" ]
  # Also allows running the workflow manually via the GitHub interface
  workflow_dispatch:

jobs:
  Explore-GitHub-Actions:
    runs-on: ubuntu-latest
    steps:
      - run: echo "🎉 The job was automatically triggered by a ${{ github.event_name }} event."
      - run: echo "🐧 This job is now running on a ${{ runner.os }} server hosted by GitHub!"
      - run: echo "🔎 The name of your branch is ${{ github.ref }} and your repository is ${{ github.repository }}."
      
      - name: Checkout repository code
        uses: actions/checkout@v4
        
      - run: echo "💡 The ${{ github.repository }} repository has been cloned to the runner."
      - run: echo "🖥️ The workflow is now ready to test your code on the runner."
        
      - name: List files in the repository
        run: |
          ls -R ${{ github.workspace }}
          
      - run: echo "🍏 This job's status is ${{ job.status }}."

## 3. Commit and Push

Save the explore_actions.yml file.
Commit and push this new file to your GitHub repository.

git add .github/workflows/explore_actions.yml
git commit -m "Add exploratory GitHub Actions workflow"
git push origin <your-branch-name>

## 4. Verify the Execution

Since you included the on: push trigger, the simple act of pushing the explore_actions.yml file will automatically start the first execution of your workflow.
To view the results:
Go to your repository on GitHub.
Click on the "Actions" tab.
You will see the new workflow listed (Explore GitHub Variables). Click on it.
Click on the most recent run and then on the Explore-GitHub-Actions job to see the output of each of your echo commands and the list of files.
