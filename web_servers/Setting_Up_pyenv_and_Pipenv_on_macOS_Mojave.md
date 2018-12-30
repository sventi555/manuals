# Setting up pyenv/Pipenv on macOS Mojave

## Overview
In this guide, we will be installing and configuring pyenv and Pipenv to be used in Python projects on macOS Mojave. These tools are especially handy due to their versatility in Python versioning and unique approach to spawning virtual environments.


## Requirements
- System running macOS 10.14.2+


## Process
### Step 1: Installing Homebrew

You can skip this step if you already have Homebrew installed on your system. Otherwise, open a terminal session and enter the following command to install Homebrew:

```
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

To confirm that it installed correctly, enter `brew`, and you should be shown a list of commands.

### Step 2: Installing Prerequisites

For pyenv and, subsequently, Python to install correctly, we need to install some prerequisites and add a few lines to our *.bash_profile*. 

First, we need to install **zlib** to decompress future packages. We can do this by entering:

```
$ brew install zlib
```

**Note** You will be instructed to run `export` commands, but don't worry. We will be adding these to our *.bash_profile* later.

Next, we must install the Xcode Command Line Tools:

```
$ xcode-select --install
```

The last thing we need to install in advance is optional, but if you will be working with sqlite databases in future Python projects, it is necessary to install now. It can be done simply with Homebrew:

```
$ brew install sqlite
```

We will take the time now to add the necessary lines to our bash profile. Open it for editing with:

```
$ vim ~/.bash_profile
```

Now add the following lines:
```
export PATH="/usr/local/opt/openssl/bin:$PATH"  
export LDFLAGS="-L/usr/local/opt/openssl/lib"
export CPPFLAGS="-I/usr/local/opt/openssl/include"
export LDFLAGS="-L/usr/local/opt/readline/lib"
export CPPFLAGS="-I/usr/local/opt/readline/include"
export PKG_CONFIG_PATH="/usr/local/opt/openssl/lib/pkgconfig"
export LDFLAGS="-L/usr/local/opt/zlib/lib"
export CPPFLAGS="-I/usr/local/opt/zlib/include"
export PKG_CONFIG_PATH="/usr/local/opt/zlib/lib/pkgconfig"
export PATH="/usr/local/opt/sqlite/bin:$PATH"
export LDFLAGS="-L/usr/local/opt/sqlite/lib"
export CPPFLAGS="-I/usr/local/opt/sqlite/include"
export PKG_CONFIG_PATH="/usr/local/opt/sqlite/lib/pkgconfig"
export CFLAGS="-I$(xcrun --show-sdk-path)/usr/include"
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
 ```

 **IMPORTANT**: Make sure you restart your terminal session before moving on, or run `source ~/.bash_profile`, otherwise the changes will not take effect.

 **Note**: This is simply my *.bash_profile* after having copied in all the prompts produced by Homebrew and others needed to execute Python through pyenv. To be safe, you should ensure that all `export` prompts are included in your *.bash_profile*.

 ### Step 3: Installing pyenv
 This is actually the easiest step in the process. We just need to install pyenv using Homebrew:

 ```
 $ brew install pyenv
 ```

 To ensure that the installation succeeded, type `pyenv` to see a list of commands.

 ### Step 4: Install Python

 We will now utilize pyenv to install the Python version of your choosing. To do this, enter this command, where `x.x.x` is the version number:

 ```
 $ pyenv install -v x.x.x
 ```

To check for success, type `pyenv versions` and you should see the specified version listed as an option.

Now to change the system-wide Python version to the one just installed, enter the following, once again making sure to replace x.x.x with your version number:

```
$ pyenv global x.x.x
```

You should now be able to enter `python` and be greeted with a Python shell using the version we just installed, looking something like this (my current version is 3.7.1):

```
Python 3.7.1 (default, Dec 28 2018, 18:48:13) 
[Clang 10.0.0 (clang-1000.11.45.5)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

### Step 5: Installing Pipenv
Now, we simply use pip to install Pipenv, as it is a Python package.

```
$ pip install pipenv
```

Check that it installed successfully by entering `pipenv`.

You can now use Pipenv to create virtual environments by entering `pipenv install`, which will create two files, *Pipfile*, and *Pipfile.lock*

To execute commands from the virtual environment, it can be activated with `pipenv shell`, or individual commands can be executed with `pipenv run "COMMAND"`, replacing "COMMAND" with your python command.


## Wrap-up
We have now finished installing and setting up pyenv and Pipenv on our macOS system. When needed, we can conveniently add different versions of Python and switch between them at will using pyenv. Also, pipenv can be utilized to easily keep track of project dependicies, and set up virtual environments. 