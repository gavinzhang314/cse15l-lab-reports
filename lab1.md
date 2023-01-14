# Lab Report 1: Remote Access Tutorial

By Gavin Zhang

## Step 1: Installing Visual Studio Code

First, we need to set up Visual Studio Code. After downloading the installer [here](https://code.visualstudio.com/Download), run the installer and follow the instructions. Once Visual Studio Code has been installed, open it. You should see something like this:

<img width="1025" alt="image" src="https://user-images.githubusercontent.com/122562285/212159124-d62fd789-5228-440a-9e8c-04a433ca1e3f.png">

## Step 2: Remotely Connecting

Now, we can open a terminal in Visual Studio Code, which we will use to remotely access your account. On Mac OS, this can be done by pressing Control+Shift+`. Additionally, there should be a "New Terminal" button in the "Terminal" menu in the menubar.

<img width="1025" alt="Screen Shot 2023-01-12 at 11 17 17 AM" src="https://user-images.githubusercontent.com/122562285/212160586-8028e6a8-a480-4cc3-b2d1-5a3d5b53f12d.png">

To connect remotely to your account, we need to use `ssh`. With the terminal open, type `ssh`, then a space, and then the username of you CSE 15L account followed by `@ieng6.ucsd.edu`. Your command should look something like this

```
ssh cse15l23w__@ieng5.ucsd.edu
```

except with the rest of your username instead of the underscores.

After clickling enter to run the command, you should be prompted for your password. Note that when you enter in your password, nothing that you enter in will show up. This is intentional. You may then be asked to confirm that you want to connect; you should type 'yes' to continue.

You should then see the following message, and finally a command prompt. 

<img width="703" alt="image" src="https://user-images.githubusercontent.com/122562285/212229994-581b4aeb-24e5-4dab-823c-8f635dc6e5cc.png">

## Step 3: Running commands

You should now be able to run commands remotely. Here are some commands I ran to navigate some directories and copy a file into my home directory:

<img width="631" alt="image" src="https://user-images.githubusercontent.com/122562285/212231123-1f425192-9691-4acb-a3dd-78a024b63432.png">
