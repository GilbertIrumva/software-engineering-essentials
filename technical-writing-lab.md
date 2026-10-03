Technical Writing Lab
Name: Gilbert
Course: Software Engineering Essentials
A) User Manual Procedure
Setting Up a GitHub Repository and Making a First Commit
1. Purpose
This procedure explains how to create a GitHub repository, connect it to a project on your computer, and make your first Git commit.
Git is a tool that tracks changes in files. GitHub is an online platform where Git repositories can be stored and shared. In this procedure, you will create a simple project and upload it to GitHub.
This guide is written for a first-semester computing student who has basic computer skills but has not used Git or GitHub before.
2. Prerequisites
Before starting, make sure you have the following:
A computer connected to the internet.
A GitHub account.
Git installed on your computer.
Git Bash or another terminal that supports Git commands.
A web browser such as Chrome, Edge, or Firefox.
Basic knowledge of opening folders and applications.
Permission to create files and folders on your computer.
You can check whether Git is installed by opening Git Bash and running:
git --version

Expected result: The terminal displays the installed Git version.
3. Procedure
Step 1: Open GitHub
Open your web browser and go to the GitHub website.
Expected result: The GitHub website opens in the browser.
Step 2: Sign in to GitHub
Sign in using your GitHub account.
Expected result: Your GitHub account opens.
Step 3: Open the new repository page
Select New repository on GitHub.
Expected result: GitHub displays the page for creating a new repository.
Step 4: Enter the repository name
Enter my-first-repository in the repository name field.
Expected result: my-first-repository appears as the repository name.
Step 5: Create the repository
Select Create repository.
Expected result: GitHub creates the repository and displays its repository page.
Step 6: Open Git Bash
Open Git Bash on your computer.
Expected result: A Git Bash terminal window opens and displays a command prompt.
Step 7: Create a project folder
Run the following command:
mkdir my-first-project

Expected result: A folder named my-first-project is created.
Step 8: Enter the project folder
Run the following command:
cd my-first-project

Expected result: The terminal is now working inside the my-first-project folder.
Step 9: Create a README file
Run the following command:
echo "# My First Project" > README.md

Expected result: A file named README.md is created inside the project folder.
Step 10: Initialize Git
Run the following command:
git init

Expected result: Git creates a local repository inside the project folder.
Step 11: Check the repository status
Run the following command:
git status

Expected result: Git shows that README.md is an untracked file.
Step 12: Stage the README file
Run the following command:
git add README.md

Expected result: Git adds README.md to the staging area.
Step 13: Check the repository status again
Run the following command:
git status

Expected result: Git shows README.md as a file that is ready to be committed.
Step 14: Create the first commit
Run the following command:
git commit -m "Initial commit"

Expected result: Git creates a commit with the message Initial commit.
Step 15: Connect the local repository to GitHub
Run the following command, replacing YOUR_USERNAME with your GitHub username:
git remote add origin https://github.com/YOUR_USERNAME/my-first-repository.git

Expected result: The local repository is connected to the GitHub repository.
Step 16: Rename the branch to main
Run the following command:
git branch -M main

Expected result: The current Git branch is renamed to main.
Step 17: Push the commit to GitHub
Run the following command:
git push -u origin main

Expected result: Git uploads the local commit and the README.md file to the GitHub repository.
Step 18: Open the GitHub repository
Open the my-first-repository page in your web browser.
Expected result: The GitHub repository page displays the README.md file and shows the Initial commit in the repository history.
4. Screenshot Description
Include a screenshot of the GitHub repository after completing Step 18.
The screenshot should show:
The repository name my-first-repository.
The README.md file.
The Initial commit message.
The main branch.
This screenshot provides evidence that the repository was successfully created and that the first commit was uploaded from the computer to GitHub.
5. Troubleshooting
Common Error: Authentication or permission error when pushing to GitHub
A beginner may receive an error when running:
git push -u origin main

This can happen when GitHub cannot authenticate the user or when the user does not have permission to access the repository.
First, check that the repository URL contains the correct GitHub username and repository name. Also make sure that the GitHub account being used has permission to access the repository.
If GitHub asks for authentication, follow the authentication instructions provided by GitHub or the Git credential manager.
After authentication is successful, run the push command again:
git push -u origin main

Expected result: The commit and project files are uploaded to GitHub.
6. Completion Check
The procedure is complete when:
A GitHub repository named my-first-repository exists.
A local project folder named my-first-project exists.
Git is initialized in the project folder.
README.md has been created.
The first commit is named Initial commit.
The local repository is connected to GitHub.
The main branch has been pushed to GitHub.
The README.md file is visible in the GitHub repository.
B) API Reference Entry
Create a New Task
1. Endpoint
HTTP Method: POST
Endpoint Path:
/api/projects/{projectId}/tasks

2. Description
This endpoint creates a new task inside a specific project.
The user must be authenticated before using this endpoint. The request must include the task title, assignee user ID, due date, and priority. The task description is optional.
After the task is created successfully, the API returns the new task, including its unique task ID and creation date.
3. Authentication
This endpoint requires an authenticated user.
The client must send an access token in the Authorization header.
Authorization: Bearer YOUR_ACCESS_TOKEN

The word Bearer must appear before the access token.
4. Request Parameters
Path Parameter
Name
Type
Required
Description
projectId
string
Yes
The unique ID of the project where the new task will be created.

Example:
/api/projects/proj_1024/tasks

In this example, proj_1024 is the project ID.
Query Parameters
This endpoint does not require any query parameters.
Request Body Parameters
The request body must be sent as JSON.
Name
Type
Required
Description
title
string
Yes
The name or title of the task.
description
string
No
Additional information about the task.
assigneeId
string
Yes
The unique ID of the user who will be responsible for the task.
dueDate
string
Yes
The date when the task should be completed. The date must use the YYYY-MM-DD format.
priority
string
Yes
The priority of the task. Allowed values are low, medium, and high.

5. Required Request Headers
The request must include the following headers:
Header
Required
Description
Authorization
Yes
Contains the user's access token.
Content-Type
Yes
Tells the server that the request body is JSON.

Example:
Authorization: Bearer eyJhbGciOiJIUzI1NiIs...
Content-Type: application/json

6. Example Request
The following example creates a high-priority task for the user with ID user_7845.
Request:
POST /api/projects/proj_1024/tasks
Authorization: Bearer eyJhbGciOiJIUzI1NiIs...
Content-Type: application/json

Request Body:
{
  "title": "Prepare project presentation",
  "description": "Create the slides and review the project results before the client meeting.",
  "assigneeId": "user_7845",
  "dueDate": "2026-10-15",
  "priority": "high"
}

The description field is optional. The other four fields are required.
7. Response Codes
The endpoint can return the following HTTP status codes.
201 Created
The task was created successfully. The response contains the newly created task.
400 Bad Request
The request contains invalid or missing information.
For example, this can happen when the title is missing or when priority contains a value other than low, medium, or high.
401 Unauthorized
The request does not contain a valid authentication token.
This can happen when the Authorization header is missing or the access token has expired.
403 Forbidden
The user is authenticated but does not have permission to create a task in the specified project.
404 Not Found
The specified project or assignee user does not exist.
405 Method Not Allowed
The client uses an HTTP method that is not supported by this endpoint.
For example, this response may occur if the client sends a GET request instead of a POST request.
409 Conflict
The request conflicts with existing data or a project rule.
For example, the API may return this response if the task cannot be created because of a conflicting operation.
415 Unsupported Media Type
The request uses a content type that the API does not support.
For example, this can happen when the client sends the request body as plain text instead of JSON.
422 Unprocessable Entity
The request has the correct structure, but one or more values cannot be accepted.
For example, the due date may have the correct format but may not meet the application's validation rules.
500 Internal Server Error
The server encountered an unexpected problem while processing the request.
This usually indicates a problem on the server rather than a problem with the client's request.
8. Example Successful Response
When the task is created successfully, the API returns 201 Created.
{
  "id": "task_58321",
  "projectId": "proj_1024",
  "title": "Prepare project presentation",
  "description": "Create the slides and review the project results before the client meeting.",
  "assigneeId": "user_7845",
  "dueDate": "2026-10-15",
  "priority": "high",
  "status": "todo",
  "createdAt": "2026-10-03T08:42:15Z"
}

9. Response Fields
Field
Type
Description
id
string
The unique ID assigned to the new task.
projectId
string
The ID of the project containing the task.
title
string
The title of the task.
description
string
Additional information about the task.
assigneeId
string
The ID of the user assigned to the task.
dueDate
string
The task's due date in YYYY-MM-DD format.
priority
string
The task priority: low, medium, or high.
status
string
The current task status. A newly created task starts with todo.
createdAt
string
The date and time when the task was created, using ISO 8601 format.

10. Summary
To create a task, the client sends a POST request to:
/api/projects/{projectId}/tasks

The request must include an authentication token and a JSON body containing title, assigneeId, dueDate, and priority. The description field is optional.
If the task is created successfully, the API returns 201 Created together with the details of the new task.


