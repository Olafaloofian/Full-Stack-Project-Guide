# Milestone Project Group Work Guide
To complete this project successfuly, you will have to use GitHub as a collaborative tool and develop some strategies for working together with your team. Here are some tips for how to go about it.

## Initial setup
Choose one person to start the repo. They should:
- [Create a repo](https://github.com/new) on GitHub for the project
- Add all the other members as collaborators in the repo's settings
- `cd` to the chosen parent directory in a terminal
- Run `npx create-react-app <appname>` to generate some starter code
- Go into the create-react-app repo with `cd <appname>`
- Link the repo to the code for the project with the following commands in your terminal (cd into the project):
  ```
  git add .
  git commit -m "initial commit"
  git remote add origin <url_of_new_repo>
  git branch -M master
  git push -u origin master

## Example starting folder structure
A lot of your project structure will come from the pre-existing create-react-app code. If you and your team want a different folder structure than the one suggested here, feel free to experiment!
- In this example, you would create the **server** folder to hold your Node server code
- Use an **.env** file in the root directory if needed for API keys or other secrest
- Certain files and directories will be automatically installed with `npm i`, including **node_modules** and **package-lock.json**
- No matter which structure you end up with, keep it in mind when importing modules and components
```
│ node_modules
│ server
├── index.js
├── controllers
│   ├── <route>.js
├── migrations
│   ├── <migration>.js
├── models
│   ├── <model>.js
│ public
├── favicon.ico
├── index.html
├── manifest.json
├── robots.txt
│ src
├── components
│   ├── <component>.jsx
│   ├── <component>.css
├── App.jsx
├── App.test.js
├── index.css
├── index.js
├── reportWebVitals.js
├── setupTests.js
│ .gitignore
│ .env
│ package-lock.json
│ package.json
│ README.md
```

## Group setup
Everyone else should:
- `cd` to the chosen parent directory in a terminal
- Clone directly from the repo (do NOT fork) with `git clone <repo_url>`
- Go into the new project folder with `cd <appname>`
- Run `npm install`
- Add any missing required files or folders from **.gitignore** (may not be needed)
- If desired, make your own branch with `git checkout -b <branchname>` (you can use your name as a branch name)

## Developing
Always make sure to add and commit along the way!
- When you have a feature done, push it to the GitHub repo from your branch with `git push`
- If your branch isn't already on the remote repo use `git push --set-upstream origin <branchname>`
- When you have a critical feature done in your branch, checkout to the main branch with `git checkout main`
- Merge the completed feature into main with `git merge <branchname>`
- Push the main branch to the repo `git push`
- Depending on the settings of the repo, this might open a pull request for the repo owner to review
- Tell your team that you have new code in the ***main*** branch

## Updating your code
When a teammates says **main** has been updated and you want the code in your branch:
- Add and commit your work with `git add .` & `git commit -m "<message>"`
- Run `git pull origin main` while checked out to your branch

## Merge conflics
If you need to resolve merge conflics:
- You will get some indication near the conflicted file names in VS Code
- Try to work through them file by file with your team
  - Click the link at the top for "Accept Current Change" or "Accept Incoming Change" (depeding on which is more correct)
- Once resolved: `git add .`, `git commit -m "commit after merge"`, `git push`

## General tips
- Use the first 5-10 minutes in class for a "standup meeting" and allow each team member to talk about:
  - What you have accomplished so far
  - What you are planning on working on
  - Struggles you are facing
- Try to separate work out as much as possible to avoid merge conflicts. Here are some suggestions:
  - Use a kanban board ([Trello](https://trello.com/) or [GitHub Project](https://docs.github.com/en/issues/planning-and-tracking-with-projects/creating-projects/creating-a-project))
  - Have people work in completely different areas of the app (React, Node, database, styling)
  - Make sure not to work in the same file
- When ready to incorporate a database, try to get it hosted as fast as possible and update the app code with the live connection string
    - This will allow you to all use the same data and not have to share backup files any time there is a schema update
    - You can use the following resources for free database hosting:
        - [Atlas](https://www.mongodb.com/cloud/atlas/register) (MongoDB)
        - [Supabase](https://supabase.com/database) (PostgreSQL)
- Always always ALWAYS stay in contact with each other about the project. Communication is key!
- Have documetation and resources ready to go if you need them
- If you are stuck on something for a while:
  - First ask if anyone else on your team can help (use screenshare or a VS Code live server to help each other)
  - Ask for help through Zoom and the instructor or associate will be there as soon as possible