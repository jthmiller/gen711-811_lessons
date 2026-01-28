## Lab 1 (take home lab, 01/27/25)

**Step 1. Sign up for a GitHub account [here](https://github.com)**
To sign up for a GitHub account as a student or faculty member at the University of New Hampshire (UNH), you should use your university email address to take advantage of educational benefits, such as the GitHub Student Developer Pack. Follow the instructions provided by GitHub. 

**Step 2. Download and install Visual Studio Code (VScode) from** [here](https://code.visualstudio.com/Download). If prompted, choose VS Code the Default Editor. 

**Step 3. Open VScode to install the **Remote SSH** extension from the Visual Studio Marketplace:**
  1. Open up vscode and click the 'building blocks' icon on the left hand side of vscode 
  2. In the upper left search bar, type 'Remote SSH'
  3. Click 'install'
  4. **For Windows users only:** Install Git from the [GitHub Pull Requests and Issues extension](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github). Once you've installed the GitHub Pull Requests and Issues extension, you'll need to sign in. Follow the prompts to authenticate with GitHub and return to VS Code. NOTE: Most versions of MacOS will already have Git installed, and you can activate it through the terminal with git version. However, if you don't have Git installed for whatever reason, you can install the latest version of Git using one of several popular methods [here](https://github.com/git-guides/install-git). 

**Step 4. Use VScode to establish a connection with RON HPC (High Performance Computing) server through vscode to set your password [see here](https://code.visualstudio.com/docs/remote/ssh).** 
Note: If you have problems with this step, skip to step 6. For this step, go to the terminal drop down menu in VScode and select 'New Terminal'. In the terminal below, run the SSH command using your username and the network address (interet address for UNH's HPC) as shown below. Replace "username" with your actual USNH username (see example for my username below that).

  ```   
  ssh username@ron.sr.unh.edu
  ```
  For me to connect I would instead use (do not use this yourself):
  ```
  ssh jtm1171@ron.sr.unh.edu
  ```

After you press enter, you'll be prompted for your password. Note that it likely won't show any indication that you're typing your password. If you mistype your password too many times in too short of a period, the server will block further connections. If this does happen, you can use the USNH VPN to bypass the block and try again. You don't normally need the VPN to connect to Ron though, whether at home or on campus.

If you experience an error connecting to Ron reporting that the host key doesn't match, this is because you likely had account on the previous version of the Ron server that was replaced last year.  To fix this error, you can remove the offending SSH host key with the following command (run this from your terminal window):
``` 
ssh-keygen -R ron.sr.unh.edu
``` 
After removing the key, the first time you connect to Ron, it will confirm that you want to save the new key. Respond 'yes' and it won't ask again.
Note: You only have to run this command if you're experiencing a host key error when connecting to Ron - please disregard if you're connecting to Ron successfully

Once connected, you will be using Bash (the shell).  If you're unfamiliar with using Bash or Linux commands in general, please review this tutorial video series. There are many videos, but you'll want to focus on videos [1-10](https://nam12.safelinks.protection.outlook.com/?url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DIrl8VXxqs8o%26list%3DPLLV_tmUM69VA4B0DKfNEBsaL9ARlpp__W%26index%3D2&data=05%7C02%7CJeffrey.Miller%40unh.edu%7C3753a6ba58c342aa545f08de5dd942c8%7Cd6241893512d46dc8d2bbe47e25f5666%7C0%7C0%7C639051384859528675%7CUnknown%7CTWFpbGZsb3d8eyJFbXB0eU1hcGkiOnRydWUsIlYiOiIwLjAuMDAwMCIsIlAiOiJXaW4zMiIsIkFOIjoiTWFpbCIsIldUIjoyfQ%3D%3D%7C0%7C%7C%7C&sdata=iwF0UJEwE%2Bgxw5hVeMMRGdmwJDls76KnLyi3UVrIXcw%3D&reserved=0)

**Step 5. Set up remote-ssh in VScode so that you can connect to RON without having to do these extra steps in the future:**  
  1. Open Remote-SSH from VScode's command palette: In VScode, open the 'command palette' by pressing 'CMD + Shift + P'. A little bar at the top of the screen should pop up. Begin to type 'Remote-SSH' and before you get too far, you should see 'Remote-SSH: Add New SSH Host...' option pop-up. Click it. If you are asked what the host operating system is, click **LINUX**

  2. Enter ssh connection command: Your command will be 'ssh' and your username (student id) will be entered into the dialog box as follows (just like above): 
  ```   
  ssh username@ron.sr.unh.edu
  ```
  But, replace "username" with your actual USNH username (see example for me below). 
  ```
  ssh jtm1171@ron.sr.unh.edu
  ```
  After you press enter, you'll may be prompted for which config file to use. For now, select the first one in the list. You should see a dialog box that says 'host added!'
  
  3. Connect to the host: Once again, open Remote-SSH's commands from VScode's command palette by pressing 'CMD + Shift + P'. This time, you want 'Remote-SSH: Connect Current Window to Host...'. You will be prompted for your password. If this all works, congrats. You will have a much shorter Lab 1 this week. Steps 6 and 7 will be performed in lab as well. 
  
**Step 6. Fork the Gen711/811 Lab Repository**
  1. Sign in to your GitHub account.
  2. From a from your GitHub account, you will need to **fork** this repository: https://github.com/jthmiller/gen711-811.git** ![fork image](../images/fork.png) Note: If you can't find the 'fork' button, you can try this [shortcut](https://github.com/jthmiller/gen711-811/fork)    
  3. In your web browser, navigate back to your own GitHub page. Login to GitHub if needed and click on your username in the top left of the screen to ensure that you are at your own github page. Then change the tab in the top left from 'Overview' to the 'Repositories'. If you forked 'gen711-811' in step 2, you should see 'gen711-811' listed in among your repositories. Click on it, and then click on the green '<> Code' dropdown button and copy the HTTPS address of your Clone (the address should look like https://github.com/jthmiller/gen711-811.git). We will use this address to run a command at RON to copy this directory there using the command line.
  
**Step 7. Clone the gen711-811 github repo into your home directory on RON:**
If you completed all other steps successfully and hope to leave lab a little earlier than most, try this final task. In VSCode, you should see a little box for typing ssh commands on the bottom right. In the terminal that is connected to RON, we will run the clone command. It should look something like this:   
``` 
git clone https://github.com/YOURUSERNAME/gen711-811.git
``` 
This should have resulted in some indication that everything downloaded. If you'd like to confirm that it worked, you can use the 'ls' command. Simply type 'ls' into the terminal connected to RON, and you should see the directory listed. Good luck!
```
ls
```

<center><b> Important!<br>To get credit for lab 1, submit a link (canvas) to your GitHub page. </b></center>


