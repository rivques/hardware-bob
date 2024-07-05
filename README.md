# bag-store-template
A template repo for a store bot using Slack and @hackclub/bag.
## Tutorial
# How to run your own store bot
Hi! This will teach you how to set up your own Bag store. We'll host it on Nest, Hack Club's program for free compute for teens.
## Prerequisites
* A [Nest]() account. Follow the [Quickstart](https://guides.hackclub.app/index.php/Quickstart) to get an account if you don't have one already.
* An editor. I reccomend VS Code with the Remote SSH extension, but you could use something like `nano` or `vim` if you're more hardcore than me.
## Sign into your Nest account
(if you're not using VS Code, connection to Nest is beyond the scope of this guide. I trust you.)

Open VS Code, install the Remote SSH extenson and click the blue >< symbol in the bottom left corner. Click "Connect current window to host," then "Add new SSH host." Enter `ssh NESTUSERNAME@NESTUSERNAME.hackclub.app`, replacing NESTUSERNAME with your Nest username. Hit enter, then enter again, then click "connect" in the notification in the bottom-right corner. A new window will open. Select "Linux" on the prompt, then "Continue". You should now find yourself logged into Nest.
## Template and clone this repository
Head to https://github.com/rivques/bag-store-template (if you're not already here). Click "Use this template" in the top right, then "Create a new repository." Change "repository name" to whatever you'd like the name of your NPC to be, and hit "Create repository." Once your repository is created, hit the big green "Code" button, then copy the url. Head back into VS Code and hit ``Ctrl+`​`` (that's the backtick) to bring up a terminal. Type `git clone URL`, replacing URL with what you just copied, and hit enter. Finally, open the folder from VS Code by heading to `File->Open Folder`, then selecting the repository you just cloned.
## Install dependencies
In the terminal, type `npm i` and hit enter.
## Create config.json
Copy the `config.json.example` file on the left sidebar and rename it to `config.json`. This is where all of your API keys will go, as well as settings like what you'll be selling. We'll fill it up over the next few steps.
## Set up Slack app
First, we need to get ourselves a Slack app. Head to the [Your Slack Apps](https://api.slack.com/apps) page and hit "Create New App," then "From App Manifest."
## Set up Bag app
Next, we need to register an app with Bag. Head to the Slack and run /bot somewhere. Enter your bot's name, then choose "public" and "read," and hit "create."

![screenshot of Bag app creation dialog](https://github.com/rivques/RPGPT/assets/38469076/f6e7ff0a-c076-49a5-8687-a2b1cf286db1)

Bag should immediately DM you an app ID and app token. Put the app ID in your `config.json` file next to `"BAG_APP_ID": `. Put the app token in to `BAG_APP_KEY`, replacing the example key. While you're in the Slack, click on your profile picture in the bottom left, then click "profile." Select the three vertical dots in the menu that pops up, then pick "Copy member ID." Paste this next to `YOUR_USER_ID` in the `config.json` file.
## Finish setting up Slack app
Head back to the Slack app page and hit "Install to workspace," then "Allow." Now, when you go back to "OAuth & Permissions," you should see a "Bot User OAuth Token." Copy that and put it in your `config.json` file for `SLACK_BOT_TOKEN`.

Now, it's time to start your bot. In the terminal, run `npm start`. Head to #market and give your bot a mention, and make sure it works.
## Set up to run 
Open bag-store.service. Replace where it says YOUR_DIRECTORY_HERE with the directory you're working in. (it'll probably look something like `/home/yournestusername/yourrepositoryname`.) Then, run the following in the terminal, one by one:
```
cp bag-store.service ~/.config/systemd/user/bag-store.service
systemctl daemon-reload
systemctl --user enable bag-store
systemctl --user start bag-store
```
This should start the bot for good.