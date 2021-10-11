---
title: Python in VSC
permalink: /docs/bops-task1/
---

### Python & Visual Studio Code

We're going to be programming in the Python programming language in this module. 

#### Visual Studio Code

Visual Studio Code (VSC) is an text based code editor. It is available for Windows, Linux and Mac from [https://code.visualstudio.com/](https://code.visualstudio.com/).  

VSC has many extensions available for it, making it usable as an editor for most programming languages, scripting and most other things.  

We'll be using the extensions listed below
* Python v2021.10.1317843341
* Pylance v2021.10.0
* Code Runner v0.11.6
* GitLens v11.6.0
  
You might find the extensions below useful
* Bracket Pair Colourizer v1.0.61
* PlantUML v2.15.1
* Prettier - Code Formatter v.9.0.0

NB These are the version numbers I have installed. There may be newer versions.  

**Installing Extensions**

When you have VSC open click on the Extensions button in the icon bar down the left hand side of the screen.  

<centre>        
    <img src="{{ "/assets/img/vsc-ext.png" | relative_url }}" alt="VSC Button Bar" class="img-responsive">
</centre>
<BR>
<centre>        
    <img src="{{ "/assets/img/ext-btn.png" | relative_url }}" alt="VSC Button Bar - Extension Button" class="img-responsive">
</centre>

This will open up the Extensions side bar.  

<centre>        
    <img src="{{ "/assets/img/ext-bar.png" | relative_url }}" alt="VSC - Extension Bar" class="img-responsive">
</centre>

Type the name of the extension you want to install in the text box at the top of the Extension Bar and click the blue install button for the extension.  

#### GitLens

If you've installed the GitLens extension correctly there should be an icon in the bar that looks like this.  

<centre>        
    <img src="{{ "/assets/img/ext-git.png" | relative_url }}" alt="VSC Button Bar - Source Control" class="img-responsive">
</centre>

Click on the button to open the Source Control sidebar.  

<centre>        
    <img src="{{ "/assets/img/git-clone1.png" | relative_url }}" alt="VSC Button Bar - Source Control Bar" class="img-responsive">
</centre>

Click on the **Clone Repository** button and enter the URL https://github.com/andyguestysj/pyHelloWorld.git in the window that pops up.  

Create a new folder to clone the repository to and select it.  

<centre>        
    <img src="{{ "/assets/img/git-clone2.png" | relative_url }}" alt="VSC Clone Repo" class="img-responsive">
</centre>

Click the **Open** button.

<centre>        
    <img src="{{ "/assets/img/git-clone3.png" | relative_url }}" alt="VSC Clone Repo" class="img-responsive">
</centre>

You should now have a copy of the *Hello World* Python program.  

If the terminal window isn't open at the bottom of the VSC window, open it from the menu *View, Terminal*.  

To run a Python program we simply right click on the code and select **Run Code**.  

You should see the results in the output window at the bottom of the screen.

