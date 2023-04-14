# Full Stack Project Guide
To complete this project successfully, you will have to use GitHub as a collaborative tool and develop some strategies for working together with your team. Here are some tips for how to go about it.

## Initial setup
Choose one person to start the repo. They should:
- [Create a repo](https://github.com/new) on GitHub for the project
- Add all the other members as collaborators in the repo's settings
- On their computer, `cd` to the chosen parent directory in a terminal
- Run `npx create-react-app <appname>` to generate some starter code
- Go into the create-react-app repo with `cd <appname>`
- Link the repo to the code for the project with the following commands:
```
git add .
git commit -m "initial commit"
git remote add origin <url_of_new_repo>
git branch -M master
git push -u origin master
```
## Example starting folder structure
A lot of your project structure will come from the pre-existing create-react-app code. If you and your team want a different folder structure than the one suggested here, feel free to experiment!
- In this example, you would create the **server** folder to hold your Node server code
- Use an **.env** file in the root directory if needed for API keys or other secrets
- If you have a **.env** file, MAKE SURE to add it in **.gitignore** (simply type `.env` in the `# misc` section)
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
├── App.css
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
Everyone else who is not the person setting up the GitHub repo should:
- `cd` to the chosen parent directory in a terminal
- Clone directly from the repo (do NOT fork) with `git clone <repo_url>`
- Go into the new project folder with `cd <appname>`
- Run `npm install`
- Add any missing required files or folders from **.gitignore** (may not be needed)
- If desired, make your own branch with `git checkout -b <your_branchname>` (you can use your name as a branch name)

## Developing in your branch
Always make sure to add and commit along the way!
- When you have a feature done, push it to the GitHub repo from your branch with `git push`
- If your branch isn't already on the remote repo use `git push --set-upstream origin <your_branchname>`

## Pulling code from main into your branch
When a teammates says **main** has been updated and you want the code in your branch:
- Add and commit your work with `git add .` & `git commit -m "<message>"`
- Run `git pull origin main` while checked out to your branch
- If you have merge conflicts, refer to the [Merge conflicts](https://github.com/Olafaloofian/Full-Stack-Project-Guide/blob/master/README.md#merge-conflicts) section below
- Add and commit your work with `git add .` and `git commit -m "commit after merge"`
- If there are any new packages being used, run `npm i`

## Pushing code from your branch into main
When you have a critical feature done in your branch and it needs to go into **main**:
- Checkout to the main branch with `git checkout main`
- Ensure you have the latest updates with `git pull`
- Merge your branch into main with `git merge <your_branchname>`
- If you have merge conflicts, refer to the [Merge conflicts](https://github.com/Olafaloofian/Full-Stack-Project-Guide/blob/master/README.md#merge-conflicts) section below
- Add and commit your work with `git add .` and `git commit -m "commit after merge"`
- Push the main branch to the repo `git push origin main`
- Depending on the settings of the repo, this might open a pull request for the repo owner to review
- Tell your team that you have new code in the **main** branch\
- Check back out to your branch if desired with `git checkout <your_branchname>`

## Merge conflicts
If you need to resolve merge conflicts:
- You will get some indication near the conflicted file names in VS Code
- Try to work through them file by file with your team
  - Click the link at the top for "Accept Current Change" or "Accept Incoming Change" (depending on which is more correct)
- Once resolved: `git add .`, `git commit -m "commit after merge"`, and `git push`

## What to work towards early on
Your initial goal should be to establish one line of communication that runs from React->Express->Database->Express->React. Try making a GET endpoint first to render some information from the database in the React UI. Here is a full breakdown of what the app should have:
- React frontend that has a pleasant and functional UI
  - Spend a bit of time on styling (you can use a styling library if desired)
  - Use the [useEffect hook](https://reactjs.org/docs/hooks-effect.html) to make API calls to your own Node server
  - Use component architecture to create re-useable chunks of code
- Express backed built on Node.js
  - Set up routes and endpoints for specific features in your app
  - Communicate with your React frontend through API calls
  - Interact with your database though Mongoose or Sequelize
  - Must have full CRUD functionality with your database
- Database (either MongoDB or PostgreSQL)
  - Organize your data into collections or tables
  - Make sure to have all the fields and columns you need for information
  - Set up the right data types for each field or column
  
## Serving up your React code
It is possible to serve up the frontend code using your Express server. It just takes a few lines of code.
- In your terminal, run `npm run build`. After a moment, it should produce a new **build** folder in your directory
- Near the top of your Express main file, add another requirement with `const path = require("path");`
- Near where you have your middlewares, add the following line: `app.use(express.static(path.join(__dirname, "..", "build")));`
  - This assumes the folder structure recommended above. Modify the middle argument path if yours is different.
- At the very bottom of the file, after all your routes, add the following:
```
app.get('*', (req, res)=>{
    res.sendFile(path.join(__dirname, '../build/index.html'));
})
```
Now if you enter your server IP address in the browser while it is running, you should see your React app!
  
## Hosting Options
One of the project requirements is for it to be hosted. It's a bit more tricky to host a full stack project, but will be really cool once you have it! Here are some recommendations for free and paid hosting services:
- Node server
  - [Cyclic](https://app.cyclic.sh/#/join/geshan)
  - [Render](https://render.com/?utm_source=geshan.com.np)
  - [AWS Lightstail](https://lightsail.aws.amazon.com/ls/docs/en_us/articles/amazon-lightsail-quick-start-guide-nodejs) [PAID $3.5+/month]
  - [Digital Ocean](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-node-js-application-for-production-on-ubuntu-16-04) [PAID $4+/month]
  - [Heroku](https://www.heroku.com/nodejs) [PAID $5+/month]
  - [AWS Beanstalk](https://aws.amazon.com/getting-started/hands-on/deploy-nodejs-web-app/) [PAID $28+/month]
- Database
  - [Atlas](https://www.mongodb.com/cloud/atlas/register) (MongoDB)
  - [Supabase](https://supabase.com/database) (PostgreSQL)
- Frontend (React)
  - [GitHub Pages](https://pages.github.com/)
  - [Vercel](https://vercel.com/)
- Domains (all paid)
  - [Namecheap](https://www.namecheap.com/)
  - [Ionos](https://www.ionos.com/)
  - [Google Domains](https://domains.google/)
  - [AWS Route 53](https://aws.amazon.com/getting-started/hands-on/get-a-domain/)

## General tips
- Use the first 5-10 minutes in class for a "standup meeting" and allow each team member to talk about:
  - What you have accomplished so far
  - What you are planning on working on
  - Struggles you are facing
- Try to distinctify work out as much as possible between teammates to avoid merge conflicts. Here are some suggestions:
  - Use a kanban board ([Trello](https://trello.com/) or [GitHub Projects](https://docs.github.com/en/issues/planning-and-tracking-with-projects/creating-projects/creating-a-project)) and assign different tasks to different people
  - Have people work in completely separate areas of the app (React, Node, database, styling)
  - Make sure not to work in the same file
- When ready to incorporate a database, try to get it hosted as fast as possible and update the app code with the live connection string
    - This will allow you to all use the same data and not have to share backup files any time there is a schema update
    - You can use the following resources for free database hosting:
        - [Atlas](https://www.mongodb.com/cloud/atlas/register) (MongoDB)
        - [Supabase](https://supabase.com/database) (PostgreSQL)
- Always always ALWAYS stay in contact with each other about the project. Communication is key!
- Have documentation and resources ready to go if you need them
- If you are stuck on something for a while:
  - First ask if anyone else on your team can help (use screenshare or a VS Code live server to help each other)
  - Ask for help through Zoom and the instructor or associate will be there as soon as possible
