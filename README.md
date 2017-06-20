mobile-dev-setup
================

<p align="center">
  <img src="https://raw.githubusercontent.com/donnemartin/dev-setup-resources/master/res/repo-header.gif">
</p>

## Motivation

Setting up a new developer machine can be an **ad-hoc, manual, and time-consuming** process.
`mobile-dev-setup` aims to **simplify** the process with **easy-to-understand instructions** and **dotfiles/scripts** to **automate the setup** for a mobile developer:

* **OS X updates and Xcode Command Line Tools**
* **OS X defaults** geared towards developers
* **Developer tools**: Vim, bash, tab completion, curl, git, GNU core utils, Python, Ruby, etc
* **Developer apps**: iTerm2, Sublime Text, Atom, Chrome, etc
* **Android development**: Java, Android SDK, Android Studio, IntelliJ IDEA

### Customisations

If you're interested in automation, `dev-setup` provides a customizable [setup script](#single-setup-script).  There's really no one-size-fits-all solution for developers so you're encouraged to make tweaks to suit your needs.

[Credits](#credits): This repo builds on the awesome work from [Donne Martin](https://github.com/donnemartin/dev-setup).


### Sections Summary
* Section 1 contains the dotfiles/scripts and instructions to set up your system.
* Sections 2 through 4 detail more information about installation, configuration, and usage for topics in Section 1.

## Section 1: Installation

**Scripts tested on OS X 10.10 Yosemite, 10.11 El Capitan & 10.12 Sierra.**

* [Single Setup Script](#single-setup-script)
* [bootstrap.sh script](#bootstrapsh-script)
    * Syncs dev-setup to your local home directory `~`
* [xcode-setup.sh script](#osxprepsh-script)
    * Updates OS X and installs Xcode command line tools
* [fresh-setup.sh script](#brewsh-script)
    * Installs common Homebrew formulae and apps
* [osx-setup.sh script](#osxsh-script)
    * Sets up OS X defaults geared towards developers
* [android-setup.sh script](#androidsh-script)
    * Sets up Android development

## Section 2: General Apps and Tools

* [Sublime Text](#sublime-text)
* [Atom](#atom)
* [Terminal Customization](#terminal-customization)
* [iTerm2](#iterm2)
* [Vim](#vim)
* [Git](#git)
* [VirtualBox](#virtualbox)
* [Vagrant](#vagrant)
* [Docker](#docker)
* [Homebrew](#homebrew)
* [Ruby and rbenv](#ruby-and-rbenv)
* [Python](#python)
* [Pip](#pip)
* [Virtualenv](#virtualenv)
* [Virtualenvwrapper](#virtualenvwrapper)

## Section 3: Android Development

* [Java](#java)
* [Android SDK](#android-sdk)
* [Android Studio](#android-studio)
* [IntelliJ IDEA](#intellij-idea)

## Section 4: Misc

* [Contributions](#contributions)
* [Credits](#credits)
* [Contact Info](#contact-info)
* [License](#license)

## Section 1: Installation

### Single Setup Script

#### Running with Git

##### Clone the Repo

    $ git clone https://github.com/donnemartin/dev-setup.git && cd dev-setup

##### Run the .dots Script with Command Line Arguments

**Since you probably don't want to install every section**, the `.dots` script supports command line arguments to run only specified sections.  Simply pass in the [scripts](#scripts) that you want to install.  Below are some examples.

**For more customization, you can [clone](#clone-the-repo) or [fork](https://github.com/gurpreetsk95/mobile-dev-setup/fork) the repo and tweak the `.dots` script and its associated components to suit your needs.**

Run all:

    $ ./.dots all

Run `bootstrap.sh`, `osxprep.sh`, `brew.sh`, and `osx.sh`:

    $ ./.dots bootstrap osxprep brew osx

Run `bootstrap.sh`, `osxprep.sh`, `brew.sh`, and `osx.sh`, `pydata.sh`, `aws.sh`, and `datastores.sh`:

    $ ./.dots bootstrap osxprep brew osx pydata aws datastores

#### Running without Git

    $ curl -O https://raw.githubusercontent.com/donnemartin/dev-setup/master/.dots && ./.dots [Add ARGS Here]

#### Scripts

* [.dots](https://github.com/gurpreetsk95/mobile-dev-setup/blob/master/.dots)
    * Runs specified scripts
* [bootstrap.sh](https://github.com/gurpreetsk95/mobile-dev-setup/blob/master/bootstrap.sh)
    * Syncs dev-setup to your local home directory `~`
* [xcode-setup.sh](https://github.com/gurpreetsk95/mobile-dev-setup/blob/master/xcode-setup.sh)
    * Updates OS X and installs Xcode command line tools
* [fresh-setup.sh](https://github.com/gurpreetsk95/mobile-dev-setup/blob/master/fresh-setup.sh)
    * Installs common Homebrew formulae and apps
* [osx-setup.sh](https://github.com/gurpreetsk95/mobile-dev-setup/blob/master/osx-setup.sh)
    * Sets up OS X defaults geared towards developers
* [android-setup.sh](https://github.com/gurpreetsk95/mobile-dev-setup/blob/master/android-setup.sh)
    * Sets up Android development

**Notes:**

* `.dots` will initially prompt you to enter your password.
* `.dots` might ask you to re-enter your password at certain stages of the installation.
* If OS X updates require a restart, simply run `.dots` again to resume where you left off.
* When installing the Xcode command line tools, a dialog box will confirm installation.
    * Once Xcode is installed, follow the instructions on the terminal to continue.
* `.dots` runs `fresh-setup.sh`, which takes awhile to complete as some formulae need to be installed from source.
* **When `.dots` completes, be sure to restart your computer for all updates to take effect.**

I encourage you to read through Section 1 so you have a better idea of what each installation script does.  The following discussions describe in greater detail what is executed when running the [.dots](https://github.com/donnemartin/dev-setup/blob/master/.dots) script.

### bootstrap.sh script

The `bootstrap.sh` script will sync the mobile-dev-setup repo to your local home directory.  This will include customizations for Vim, bash, curl, git, tab completion, aliases, a number of utility functions, etc.  Section 2 of this repo describes some of the customizations.

#### Running with Git

First, fork or [clone the repo](#clone-the-repo).  The `bootstrap.sh` script will pull in the latest version and copy the files to your home folder `~`:

    $ source bootstrap.sh

To update later on, just run that command again.

Alternatively, to update while avoiding the confirmation prompt:

    $ set -- -f; source bootstrap.sh

#### Running without Git

To sync dev-setup to your local home directory without Git, run the following:

    $ cd ~; curl -#L https://github.com/gurpreetsk95/mobile-dev-setup/tarball/master | tar -xzv --strip-components 1 --exclude={README.md,bootstrap.sh,LICENSE}

To update later on, just run that command again.

#### Optional: Specify PATH

If `~/.path` exists, it will be sourced along with the other files before any feature testing (such as detecting which version of `ls` is being used takes place.

Here’s an example `~/.path` file that adds `/usr/local/bin` to the `$PATH`:

```bash
export PATH="/usr/local/bin:$PATH"
```

#### Optional: Add Custom Commands

If `~/.extra` exists, it will be sourced along with the other files. You can use this to add a few custom commands without the need to fork this entire repository, or to add commands you don’t want to commit to a public repository.

You could also use `~/.extra` to override settings, functions, and aliases from the dev-setup repository, although it’s probably better to [fork the mobile-dev-setup repository](https://github.com/gurpreetsk95/mobile-dev-setup/fork).

### xcode-setup.sh script

Run the `xcode-setup.sh` script:

    $ ./xcode-setup.sh

`xcode-setup.sh` will first install all updates.  If a restart is required, simply run the script again.  Once all updates are installed, `xcode-setup.sh` will then [Install Xcode Command Line Tools](#install-xcode-command-line-tools).

If you want to go the manual route, you can also install all updates by running "App Store", selecting the "Updates" icon, then updating both the OS and installed apps.

#### Install Xcode Command Line Tools

An important dependency before many tools such as Homebrew can work is the **Command Line Tools for Xcode**. These include compilers like gcc that will allow you to build from source.

If you are running **OS X 10.9 Mavericks or later**, then you can install the Xcode Command Line Tools directly from the command line with:

    $ xcode-select --install

**Note**: the `xcode-setup.sh` script executes this command.

Running the command above will display a dialog where you can either:
* Install Xcode and the command line tools
* Install the command line tools only
* Cancel the install

##### OS X 10.8 and Older

If you're running 10.8 or older, you'll need to go to [http://developer.apple.com/downloads](http://developer.apple.com/downloads), and sign in with your Apple ID (the same one you use for iTunes and app purchases). Unfortunately, you're greeted by a rather annoying questionnaire. All questions are required, so feel free to answer at random.

Once you reach the downloads page, search for "command line tools", and download the latest **Command Line Tools (OS X Mountain Lion) for Xcode**. Open the **.dmg** file once it's done downloading, and double-click on the **.mpkg** installer to launch the installation. When it's done, you can unmount the disk in Finder.

### fresh-setup.sh script

When setting up a new Mac, you may want to install [Homebrew](http://brew.sh/), a package manager that simplifies installing and updating applications or libraries.

Some of the apps installed by the `fresh-setup.sh` script include: Chrome, Firefox, Sublime Text, Atom, Skype, Slack etc.  **For a full listing of installed formulae and apps, refer to the commented [fresh-setup.sh source file](https://github.com/gurpreetsk95/mobile-dev-setup/blob/master/fresh-setup.sh) directly and tweak it to suit your needs.**

Run the `fresh-setup.sh` script:

    $ ./fresh-setup.sh

The `fresh-setup.sh` script takes awhile to complete, as some formulae need to be installed from source.

**For your terminal customization to take full effect, quit and re-start the terminal**

### osx-setup.sh script

When setting up a new Mac, you may want to set OS X defaults geared towards developers.  The `osx.sh` script also configures common third-party apps such Sublime Text and Chrome.

**Note**: **I strongly encourage you read through the commented [osx-setup.sh source file](https://github.com/gurpreetsk95/mobile-dev-setup/blob/master/osx-setup.sh) and tweak any settings based on your personal preferences.  The script defaults are intended for you to customize.**  For example, if you are not running an SSD you might want to change some of the settings listed in the SSD section.

Run the `osx-setup.sh` script:

    $ ./osx-setup.sh

**For your terminal customization to take full effect, quit and re-start the terminal.**


### android-setup.sh script

<p align="center">
  <img src="https://raw.githubusercontent.com/donnemartin/dev-setup-resources/master/res/android.png">
  <br/>
</p>

To set up an Android development environment, run the `android.sh` script:

    $ ./android-setup.sh

[Section 4: Android Development](#section-4-android-development) describes the installed packages and usage.


## Section 2: General Apps and Tools

### Sublime Text

<p align="center">
  <img src="https://raw.githubusercontent.com/donnemartin/dev-setup-resources/master/res/sublime.png">
  <br/>
</p>

With the terminal, the text editor is a developer's most important tool. Everyone has their preferences, but unless you're a hardcore [Vim](http://en.wikipedia.org/wiki/Vim_(text_editor)) user, a lot of people are going to tell you that [Sublime Text](http://www.sublimetext.com/) is currently the best one out there.

#### Installation

The fresh-setup.sh script installs Sublime Text.

If you prefer to install it separately, go ahead and [download](http://www.sublimetext.com/) it. Open the **.dmg** file, drag-and-drop in the **Applications** folder.

**Note**: At this point I'm going to create a shortcut on the OS X Dock for both for Sublime Text. To do so, right-click on the running application and select **Options > Keep in Dock**.

Sublime Text is not free, but I think it has an unlimited "evaluation period". Anyhow, we're going to be using it so much that even the seemingly expensive $70 price tag is worth every penny. If you can afford it, I suggest you [support](http://www.sublimetext.com/buy) this awesome tool.

#### Configuration

The osx-setup.sh script contains Sublime Text configurations.

#### Soda Theme

The [Soda Theme](https://github.com/buymeasoda/soda-theme) is a great UI theme for Sublime Text, especially if you use a dark theme and think the side bar sticks out like a sore thumb.

##### Installation with Sublime Package Control

If you are using Will Bond's excellent [Sublime Package Control](http://wbond.net/sublime_packages/package_control), you can easily install Soda Theme via the `Package Control: Install Package` menu item. The Soda Theme package is listed as `Theme - Soda` in the packages list.

##### Installation with Git

Alternatively, if you are a git user, you can install the theme and keep up to date by cloning the repo directly into your `Packages` directory in the Sublime Text application settings area.

You can locate your Sublime Text `Packages` directory by using the menu item `Preferences -> Browse Packages...`.

While inside the `Packages` directory, clone the theme repository using the command below:

    $ git clone https://github.com/buymeasoda/soda-theme/ "Theme - Soda"

##### Activating the Theme on Sublime Text 2

* Open your User Settings Preferences file `Sublime Text 2 -> Preferences -> Settings - User`
* Add (or update) your theme entry to be `"theme": "Soda Light.sublime-theme"` or `"theme": "Soda Dark.sublime-theme"`

**Example Sublime Text 2 User Settings**

    {
        "theme": "Soda Light.sublime-theme"
    }

##### Activating the Theme on Sublime Text 3

* Open your User Settings Preferences file `Sublime Text -> Preferences -> Settings - User`
* Add (or update) your theme entry to be `"theme": "Soda Light 3.sublime-theme"` or `"theme": "Soda Dark 3.sublime-theme"`

**Example Sublime Text 3 User Settings**

    {
        "theme": "Soda Light 3.sublime-theme"
    }

##### Changing Monokai Comment Color

Although Monokai is a great color scheme, I find that comments can be difficult to see.  You can follow these [instructions](http://stackoverflow.com/a/32686509) to change the color of the default theme.

I set my comments color to `#E6DB74`.

```
<dict>
    ...
    <dict>
        <key>foreground</key>
        <string>#E6DB74</string>
    </dict>
    ...
</dict>
```

### Atom

<p align="center">
  <img src="https://raw.githubusercontent.com/donnemartin/dev-setup-resources/master/res/atom.png">
  <br/>
</p>

[Atom](https://github.com/atom/atom) is a great open-source editor from GitHub that is rapidly gaining contributors and popularity.

#### Installation

The fresh-setup.sh script installs Atom.

If you prefer to install it separately, [download](https://atom.io/) it, open the **.dmg** file, drag-and-drop in the **Applications** folder.

#### Configuration

Atom has a great package manager that allows you to easily install both core and community packages.

### Terminal Customization

<p align="center">
  <img src="https://raw.githubusercontent.com/donnemartin/dev-setup-resources/master/res/terminal.png">
  <br/>
</p>

Since we spend so much time in the terminal, we should try to make it a more pleasant and colorful place.

#### Configuration

The [bootstrap.sh script](#bootstrapsh-script) and [osx.sh script](#osxsh-script) contain terminal customizations.

### iTerm2

<p align="center">
  <img src="https://raw.githubusercontent.com/donnemartin/dev-setup-resources/master/res/iterm2.png">
  <br/>
</p>

I prefer iTerm2 over the stock Terminal, as it has some additional [great features](https://www.iterm2.com/features.html). Download and install iTerm2 (the newest version, even if it says "beta release").

In Finder, drag and drop the iTerm Application file into the Applications folder.

You can now launch iTerm, through the Launchpad for instance.

Let's just quickly change some preferences. In iTerm > Preferences..., in the tab Profiles, create a new one with the "+" icon, and rename it to your first name for example. Then, select Other Actions... > Set as Default. Under the section Window, change the size to something better, like Columns: 125 and Rows: 35.  I also like to set General > Working Directory > Reuse previous session's directory.  Finally, I change the way the option key works so that I can quickly jump between words as described [here](https://coderwall.com/p/h6yfda/use-and-to-jump-forwards-backwards-words-in-iterm-2-on-os-x).

When done, hit the red "X" in the upper left (saving is automatic in OS X preference panes). Close the window and open a new one to see the size change.

#### Configuration

Since we spend so much time in the terminal, we should try to make it a more pleasant and colorful place. What follows might seem like a lot of work, but trust me, it'll make the development experience so much better.

Now let's add some color. I'm a big fan of the [Solarized](http://ethanschoonover.com/solarized) color scheme. It is supposed to be scientifically optimal for the eyes. I just find it pretty.

- In **iTerm2 Preferences**, under **Profiles** and **Colors**, go to **Load Presets...** and select **Solarized Dark** to activate it. Voila!

At this point you can also change your computer's name, which shows up in this terminal prompt. If you want to do so, go to **System Preferences** > **Sharing**. For example, I changed mine from "Donne's MacBook Pro" to just "MacBook Pro", so it shows up as `MacBook-Pro` in the terminal.

Now we have a terminal we can work with!

### Vim

<p align="center">
  <img src="https://raw.githubusercontent.com/donnemartin/dev-setup-resources/master/res/vim.png">
  <br/>
</p>

Although Sublime Text will be our main editor, it is a good idea to learn some very basic usage of [Vim](http://www.vim.org/). It is a very popular text editor inside the terminal, and is usually pre-installed on any Unix system.

For example, when you run a Git commit, it will open Vim to allow you to type the commit message.

I suggest you read a tutorial on Vim. Grasping the concept of the two "modes" of the editor, **Insert** (by pressing `i`) and **Normal** (by pressing `Esc` to exit Insert mode), will be the part that feels most unnatural. After that it's just remembering a few important keys.

#### Configuration

The [bootstrap.sh script](#bootstrapsh-script) contains Vim customizations.

### Git

<p align="center">
  <img src="https://raw.githubusercontent.com/donnemartin/dev-setup-resources/master/res/git.png">
  <br/>
</p>

What's a developer without [Git](http://git-scm.com/)?

#### Installation

Git should have been installed when you ran through the [Install Xcode Command Line Tools](#install-xcode-command-line-tools) section.

#### Configuration

To check your version of Git, run the following command:

    $ git --version

And `$ which git` should output `/usr/local/bin/git`.

Let's set up some basic configuration. Download the [.gitconfig](https://raw.githubusercontent.com/donnemartin/dev-setup/master/.gitconfig) file to your home directory:

    $ cd ~
    $ curl -O https://raw.githubusercontent.com/donnemartin/dev-setup/master/.gitconfig

It will add some color to the `status`, `branch`, and `diff` Git commands, as well as a couple aliases. Feel free to take a look at the contents of the file, and add to it to your liking.

Next, we'll define your Git user (should be the same name and email you use for [GitHub](https://github.com/) and [Heroku](http://www.heroku.com/)):

    $ git config --global user.name "Your Name Here"
    $ git config --global user.email "your_email@youremail.com"

They will get added to your `.gitconfig` file.

To push code to your GitHub repositories, we're going to use the recommended HTTPS method (versus SSH). So you don't have to type your username and password everytime, let's enable Git password caching as described [here](https://help.github.com/articles/set-up-git):

    $ git config --global credential.helper osxkeychain

**Note**: On a Mac, it is important to remember to add `.DS_Store` (a hidden OS X system file that's put in folders) to your `.gitignore` files. You can take a look at this repository's [.gitignore](https://github.com/donnemartin/dev-setup/blob/master/.gitignore) file for inspiration.  Also check out GitHub's [collection of .gitignore templates](https://github.com/github/gitignore).

### Homebrew

<p align="center">
  <img src="https://raw.githubusercontent.com/donnemartin/dev-setup-resources/master/res/homebrew.png">
  <br/>
</p>

Package managers make it so much easier to install and update applications (for Operating Systems) or libraries (for programming languages). The most popular one for OS X is [Homebrew](http://brew.sh/).

#### Installation

The [brew.sh script](#brewsh-script) installs Homebrew and a number of useful Homebrew formulae and apps.

If you prefer to install it separately, run the following command and follow the steps on the screen:

    $ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

#### Usage

To install a package (or **Formula** in Homebrew vocabulary) simply type:

    $ brew install <formula>

To update Homebrew's directory of formulae, run:

    $ brew update

**Note**: I've seen that command fail sometimes because of a bug. If that ever happens, run the following (when you have Git installed):

    $ cd /usr/local
    $ git fetch origin
    $ git reset --hard origin/master

To see if any of your packages need to be updated:

    $ brew outdated

To update a package:

    $ brew upgrade <formula>

Homebrew keeps older versions of packages installed, in case you want to roll back. That rarely is necessary, so you can do some cleanup to get rid of those old versions:

    $ brew cleanup

To see what you have installed (with their version numbers):

    $ brew list --versions

### Ruby and rbenv

<p align="center">
  <img src="https://raw.githubusercontent.com/donnemartin/dev-setup-resources/master/res/ruby.png">
  <br/>
</p>

[Ruby](http://www.ruby-lang.org/) is already installed on Unix systems, but we don't want to mess around with that installation. More importantly, we want to be able to use the latest version of Ruby.

#### Installation

`brew.sh` provides [rbenv](https://github.com/rbenv/rbenv) and [ruby-build](https://github.com/rbenv/ruby-build) which allow you to manage multiple versions of Ruby on the same machine.  `brew.sh` adds the following line to your `.extra` file to initialize `rbenv`:

```
eval "$(rbenv init -)"
```

#### Usage

`rbenv` uses `ruby-build` to download, compile, and install new versions of Ruby. You can see all versions available to download and install:

```
$ ruby-build --definitions
```

To install a new version of Ruby:

```
# list all available versions installed on the system:
$ rbenv install -l

# install a Ruby version:
$ rbenv install 2.2.3
```

To switch Ruby versions:

```
# set a local application-specific Ruby version in the current directory
$ rbenv local 1.9.3

# set the global version of Ruby to be used in all shells
$ rbenv global 2.0.0

```

`rbenv` by default will install Ruby versions into a directory of the same name under `~/.rbenv/versions`. Because your user owns this directory, you no longer need to use `sudo` to install gems.

### Python

<p align="center">
  <img src="https://raw.githubusercontent.com/donnemartin/dev-setup-resources/master/res/python.png">
  <br/>
</p>

OS X, like Linux, ships with [Python](http://python.org/) already installed. But you don't want to mess with the system Python (some system tools rely on it, etc.), so we'll install our own version with Homebrew. It will also allow us to get the very latest version of Python 2.7 and Python 3.

#### Installation

The [first-install.sh script](#brewsh-script) installs the latest versions of Python 2 and Python 3.

## Section 3: Android Development

### Java

<p align="center">
  <img src="https://raw.githubusercontent.com/donnemartin/dev-setup-resources/master/res/java.png">
  <br/>
</p>

#### Installation

The [android-setup.sh script](#androidsh-script) installs Java.

If you prefer to install it separately, you can download the JDK [here](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or run:

    $ brew update
    $ brew install caskroom/cask/brew-cask
    $ brew cask install --appdir="~/Applications" java

### Android SDK

<p align="center">
  <img src="https://raw.githubusercontent.com/donnemartin/dev-setup-resources/master/res/androidsdk.png">
  <br/>
</p>

The [android-setup.sh script](#androidsh-script) installs the Android SDK.

If you prefer to install it separately, you can download it [here](https://developer.android.com/sdk/index.html).

### Android Studio

<p align="center">
  <img src="https://raw.githubusercontent.com/donnemartin/dev-setup-resources/master/res/androidstudio.png">
  <br/>
</p>

The [android-setup.sh script](#androidsh-script) installs Android Studio.

If you prefer to install it separately, you can download it [here](https://developer.android.com/sdk/index.html) or run:

    $ brew update
    $ brew install caskroom/cask/brew-cask
    $ brew cask install --appdir="~/Applications" android-studio

### IntelliJ IDEA

<p align="center">
  <img src="https://raw.githubusercontent.com/donnemartin/dev-setup-resources/master/res/intellij.png">
  <br/>
</p>

The [android-setup.sh script](#androidsh-script) installs Java.

If you prefer to install it separately, you can download it [here](https://www.jetbrains.com/idea/download/) or run:

    $ brew update
    $ brew install caskroom/cask/brew-cask
    $ brew cask install --appdir="~/Applications" intellij-idea-ce

## Section 4: Misc

### Contributions

Bug reports, suggestions, and pull requests are [welcome](https://github.com/donnemartin/dev-setup/issues)!

### Credits

See the [Credits Page](https://github.com/donnemartin/dev-setup/blob/master/CREDITS.md).

## Contact Info

Feel free to contact me to discuss any issues, questions, or comments.

My contact info can be found on my [GitHub page](https://github.com/donnemartin).

### License

This repository contains a variety of content; some developed by Gurpreet Singh, and some from third-parties.  The third-party content is distributed under the license provided by those parties.

The content developed by Gurpreet Singh is distributed under the following license:

*I am providing code and resources in this repository to you under an open source license.  Because this is my personal repository, the license you receive to my code and resources is from me and not my employer.*

    Copyright 2017 Gurpreet Singh

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
