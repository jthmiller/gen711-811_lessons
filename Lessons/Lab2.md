## Lab 2 (1/30/26)

## Start this lab once you have access to RON through VScode

### Make repository on GitHub for your lab notebook on RON and your local computer
Now that you are connected to RON, lets make a lab notebook in your repo to be graded each week. The easiest way to do this is to first create a new repository on GitHub.com, and then clone that to your home directory on RON and your laptop.
1. Login to GitHub with the credentials you made for Lab 1
2. On your GitHub page, click 'Repositories' 
3. Click the green 'New' button
4. In 'Repository Name', type 'Bioinformatics-Notes'  **No spaces. Lets all keep the same simple name**
5. Flip the switch to 'on' for the 'Add README'
6. Click 'Create repository'

### Next, we will clone the repo on RON, and open up the folder with VScode (using the Remote SSH extension)
1. Open up vscode
2. Control + shift + 'p' to open command prompt (command + shift + p on apple)
3. Start typing 'Connect to...' and the 'Connect current window to host' menu item will pop up. Select it
4. If asked, connect to ron.sr.edu host
5. Enter your RON username if prompted
6. Enter your RON password when prompted
7. Once you are successfully connected to RON and in your home directory, clone with the 'git clone' command:
```
cd $HOME
git clone https://github.com/<YOURGITHUBUSERNAME>/Bioinformatics-Notes.git
```
You should see an indication that it downloaded ok. 

### Next, we will open the directory you cloned in VScode to save the workspace and make a lab notebook that should be the same on RON and your machine.
1. In the VScode window that you have connected to RON, go to 'File --> Open folder'
2. The command pallet in VScode should show your 'home directories' including the 'Bioinformatics-Notes' directory. Select it.  
3. If you did this correctly, you should now see the README file pop up on the left in the list of files. Click on it to open it. 
4. While we are at it, lets save your VScode workspace in the repo directory. Click 'File --> Save Workspace As...' and click on the 'Bioinformatics-Notes' directory to save the workspace there. The workspace file just lists your VScode preferences.This way, you can load this workspace each week to pick up where you left off.   
5. In vscode terminal, go to 'file' --> 'new text file'. Save this empty file as 'yourlastname_yourfirstname.md'. Keep notes in this file as demonstrated by your instructor to get full attendance points. Add some short random text to this document to make sure that it is picked up. 
6. If you've done everything above correctly, new documents and changes should be tracked VScode and Git. To get your changes incorporated into your repository at GitHub, click on the github bubble fork (usually the third icon down on the left of VScode). Enter any random text you want into the 'Message' box, and then hit the commit button. This should upload your new files/changes to your GitHub repo. 

Note: Text files saved with the '.md' after it will be interpreted at 'markdown' format. We will get into this soon. 

**Generate ssh-keys to log into RON without usernames and passwords**  

First, open 'terminal' on your mac. We are going to use the terminal to generate the keys and restrict the permissions on the private key file. For macOS / Linux, run the following shell command, replacing the path to your private key if necessary:
```
cd ~/.ssh
ssh-keygen -t ed25519 -b 4096
chmod 400 ~/.ssh/id_ed25519
```
<br>

- Next, share the public key with the Ron server
```
ssh-copy-id USERNAME@ron.sr.unh.edu
```
If that doesn't work, we can try:
```
cat ~/.ssh/id_rsa.pub | ssh user@12.34.56.78 "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys
```
</details> <!-- end for mac-->
<br>
 <details><summary>For Windows</summary> 

**For Windows**, run the following command in PowerShell to grant explicit read access to your username:
```
icacls "privateKeyPath" /grant :R
```
Then navigate to the private key file in Windows Explorer, right-click and select Properties. Select the Security tab → Advanced → Disable inheritance → Remove all inherited permissions from this object.

<br>

### Next Week

To get new course files added to your repository later, you will need to add the original repository (the one you forked) as a 'remote' [see here for help](https://stackoverflow.com/questions/3903817/pull-new-updates-from-original-github-repository-into-forked-github-repository),[and here](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo)  
To add updates from the gen711-811 repo:
```
cd gen711-811
git remote add upstream https://github.com/jthmiller/gen711-811.git
git fetch upstream
git merge upstream/master master
```
Note, git merge is like "git pull" which is fetch + merge. Or, better, you can replay your local work on top of the fetched branch like a "git pull --rebase"
```
git rebase upstream/master
```
