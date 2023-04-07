### How to create environments get started running TensorFlow and other data science libraries on Apple Silicon (Apr, 2023)
If you're new to creating environments, using a new M1, M1 Pro, M1 Max, M1 Ultra, M2 machine and would like to get started running TensorFlow and other data science libraries, follow the below steps.

> **Note:** _A **package manager** is a piece of software that helps you install other pieces (packages) of software._


After installing package managers (Homebrew and Miniforge), you will be creating a Tensorflow environment.


#### Creating a TensorFlow environment
Now we've got the package managers we need, it's time to install TensorFlow.

Let's set up a folder called _tensorflow-test_ (you can call this anything you want) and install everything in there to make sure it's working.

> Note: An environment is like a virtual room on your computer. For example, you use the kitchen in your house for cooking because it's got all the tools you need. It would be strange to have an oven in your bedroom. The same thing on your computer. If you're going to be working on specific software, you'll want it all in one place and not scattered everywhere else. 
> Make a directory called tensorflow-test.
> This is the directory we're going to be storing our environment. And inside the environment will be the software tools we need to run TensorFlow.

We can do so with the **_mkdir_** command which stands for "make directory".
```sh
mkdir tensorflow-test
```
> Note: You could call the directory here anything you want, I'm just calling it tensorflow-test for this example. If you were working on a project to classify images of dogs you might make a folder called dog-vision.

2. Change into tensorflow-test.

For the rest of the commands we'll be running them inside the directory tensorflow-test so we need to change into it.

We can do this with the cd command which stands for "change directory".
```sh
cd tensorflow-test
```
3. Create a Conda environment.

Now we're inside the tensorflow-test directory, let's create a new Conda environment using the conda command (this command was installed when we installed Miniforge above).

We do so using conda create --prefix ./env which stands for "conda create an environment with the name file/path/to/this/folder/env". The . stands for "everything before".

For example, if I didn't use the ./env, my filepath looks like: /Users/daniel/tensorflow-test/env
```sh
conda create --prefix ./env
```
4. Activate the environment.

If conda created the environment correctly, you should be able to activate it using conda activate path/to/environment.

Short version:
```sh
conda activate ./env
```

Long version:
```sh
conda activate /Users/sangayyonten/tensorflow-test/env
```
    
> Note: It's important to activate your environment every time you'd like to work on projects that use the software you install into that environment. For example, you might have one environment for every different project you work on. And all the different tools for that specific project are stored in its specific environment.

If activating your environment went correctly, your terminal window prompt should look something like:
```sh
(/Users/sangayyonten/tensorflow-test/env) sangayyonten@Sangay-MBP tensorflow-test %
```

5. Installing the software we need as in (TensorFlow and other data science packages) and start the Jupyter Notebook and test everything out.