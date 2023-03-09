## Working with multiple GitHub accounts on a single Machine

Suppose I have two GitHub accounts, **https:/<span></span>/github.com<span></span>/sangay-office** and **https:/<span></span>/github.com<span></span>/sangay-personal**. Now I want to set up my Mac to easily commit my changes to both the GitHub accounts.

> NOTE: This logic is applicable to more than two accounts too. :)

The setup can be done in 5 easy steps:
## Steps:
- [Step 1](#step-1) : Create SSH keys for all accounts
- [Step 2](#step-2) : Add SSH keys to SSH Agent
- [Step 3](#step-3) : Add SSH public key to the Github
- [Step 4](#step-4) : Create a Config File and Make Host Entries
- [Step 5](#step-5) : Cloning GitHub repositories using different accounts
<br />

## Step 1
### Create SSH keys for all the accounts

First make sure your current directory is your root **.ssh** folder.
```sh
     $ cd ~/.ssh
```
Syntax for generating unique ssh key for ann account is:
```sh
     ssh-keygen -t rsa -C "your-email-address" -f "github-username"
```
here,

**-C** stands for comment to help identify your ssh key

**-f** stands for the file name where your ssh key get saved


### Now let's generate SSH keys for the two accounts
```sh
     ssh-keygen -t rsa -C "office_email@organization.org" -f "github-sangay-office"
     ssh-keygen -t rsa -C "personal_email@gmail.com" -f "github-sangay-personal"
```

Notice that, here **sangay-office** and **sangay-personal** are the username of the GitHub accounts corresponding to **office_email<span></span>@organization.org** and **personal_email<span></span>@gmail.com** email ids respectively.

**[ Note: ]** <br />
After entering the command the terminal will ask for **passphrase**, you can leave it empty and proceed.

> Now after adding keys , in your .ssh folder, a public key and a private will get generated.

>The public key will have an extention __.pub__ and private key will be there without any extention both having same name which you have passed after __-f__ option in the above command. (in my example; __github-sangay-office__ and __github-sangay-personal__)
<br />

## Step 2
### Add SSH keys to SSH Agent
Now we have the keys, but it cannot be used until we add them to the SSH Agent.
```sh
     ssh-add -K ~/.ssh/github-rahul-office
     ssh-add -K ~/.ssh/github-rahul-personal
```

You can read more about adding keys to SSH Agent [here.](https://help.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
<br />

## Step 3
### Add SSH public key to the GitHub
For the next step we need the public key (that we have generated in our previous step) and add it to corresponding GitHub accounts.

For doing this you can proceed with the following:

__1. Copy the public key__

     We can copy the public key either by opening the github-sangay-office.pub file in vim and then copying the content of it.
```sh
     vim ~/.ssh/github-sangay-office.pub
     vim ~/.ssh/github-sangay-personal.pub
```

<p align="center">OR</p>

We can directly copy the content of the public key file in the clipboard.

```sh
     pbcopy < ~/.ssh/github-sangay-office.pub
     pbcopy < ~/.ssh/github-sangay-personal.pub
```

__2. Paste the public key on Github__

* Sign in to the respective GitHub accounts
* Go to **Settings** > **SSH and GPG keys** > **New SSH Key**
* Paste the corresponding copied public key and give it a **Title** of your choice.

___OR___

* Sign in to GitHub
* Paste this link in your browser (https://github.com/settings/keys) or click [here](https://github.com/settings/keys)
* Click on **New SSH Key** and paste the corresponding copied keys.
<br />

## Step 4
### Create a Config File and Make Host Entries

The **~/.ssh/config** file allows us to specify many config options for SSH.

If **config** file does not already exist, then create one (make sure you are in the **~/.ssh** directory)

```sh
     touch config
```
The commands below opens config in your default editor....Likely TextEdit, VS Code.
```sh
     open config
```
Now we need to add these lines to the file, each block corresponding to each account we created earlier.
```config
     #office account
     Host github.com-sangay-office
          HostName github.com
          User git
          IdentityFile ~/.ssh/github-sangay-office

     #personal account
     Host github.com-sangay-personal
          HostName github.com
          User git
          IdentityFile ~/.ssh/github-sangay-personal
```
<br />

## Step 5
### Cloning GitHub repositories using different accounts

So we are done with our setups, and now it's time to see it in action. We will clone a repository using one of the account we have added.

Make a new project folder where you want to clone your repository and go to that directory from your terminal.

For Example:
I am making a repository on my personal GitHub account and naming it **TrialRepo**
Now for cloning the repo use the below command:
 ```git
     git clone git@github.com-{your-username}:{github-user-name}/{the-repo-name}.git
 ```
**Example:**
 ```git
     git clone git@github.com-sangay-personal:sangay-personal/TrialRepo.git
 ```
 <br />

## Finally

From now on, to ensure that our commits and pushes from each repository on the system uses the correct GitHub user — we will have to configure **user.email** and **user.name** in **_[every repository*]_** freshly cloned or existing before.

To do this use the following commands;

```git
     git config user.email "office_email@organization.org"
     git config user.name "sangay-ofice"
     
     git config user.email "personal-email@gmail.com"
     git config user.name "sangay-personal"
```
Pick the correct pair for your repository accordingly.


To push or pull to the correct account we need to add the remote origin to the project
```git
    git remote add origin git@github.com-{your-username}:{github-user-name}
```
**Example:**
```git
     git remote add origin git@github.com-sangay-personal:sangay-personal
     
     git remote add origin git@github.com-sangay-office:sangay-office
```

Now you can use execute the following commands to the desired repositories:
```git
     git push
     git pull
```