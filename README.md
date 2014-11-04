---
tags: kids, setup, rvm, homebrew
type: environment setup
language: bash
---

## Environment Set Up - Part 3

###1. Installing RVM
RVM stands for Ruby Version Manager. Ruby, just like software, has newer and older versions. RVM allows you to have multiple versions of ruby installed on your computer that you can easily switch back and forth between. 

```
\curl -L https://get.rvm.io | bash -s stable --ruby=2.1.1
```

This command will install the latest version of ruby, as well as ruby 2.1.1.

Now, we want to make 2.1.1 our default version. Enter `rvm use 2.1.1 --default`. If you open a new tab and then type `ruby -v`, you should see 2.1.1

If you have issues with Homebrew, You can try reinstalling it with this command:
```
\curl -L https://gist.github.com/mxcl/1173223/raw/a833ba44e7be8428d877e58640720ff43c59dbad/uninstall_homebrew.sh | bash
```

If you get any errors related to XCode or GCC, try reinstalling XCode developer tools with this command `xcode-select --install`, then try installing RVM again. 

###2. Install RSpec
Type `gem install rspec` in your terminal.


###3. Install The Ironboard Gem
This gem isn't open-sourced, so we won't be downloading it from RubyGems.org, which is where most gems are hosted. Before we download it, we will need to specify where it's coming from, which is a private server at Flatiron. Type this into your command line;

`gem sources -a http://flatiron:33west26@gems.flatironschool.com/`

Next, download the gem:

`gem install ironboard`

The ironboard gem will help track your progress on labs.

###3. RVM and Sublime Together
To get RVM and Sublime to play nice, we need to do the following:
```
open "$HOME/Library/Application Support/Sublime Text 2/Packages/Ruby/Ruby.sublime-build"
```
Once the file is open, you'll need to paste the below into the file:
```
{
  "env":{
      "PATH":"${HOME}/.rvm/bin:${PATH}"
  },
  "cmd": ["rvm-auto-ruby", "$file"],
  "file_regex": "^(...*?):([0-9]*):?([0-9]*)",
  "selector": "source.ruby"
} 
```

###4. Update your Bash Profile
Make sure you are in your root directory by typing `cd ~` in your terminal. From here you should be able to open up your bash profile with this command `subl .bash_profile`.

Scroll down to the very bottom of your bash profile and copy and paste this code after everything else that is already in there:

```
# Final Configurations and Plugins
# =====================
  # Git Bash Completion
  # Will activate bash git completion if installed
  # via homebrew
  if [ -f `brew --prefix`/etc/bash_completion ]; then
    . `brew --prefix`/etc/bash_completion
  fi

  # RVM
  # Mandatory loading of RVM into the shell
  # This must be the last line of your bash_profile always
  [[ -s "/Users/$USER/.rvm/scripts/rvm" ]] && source "/Users/$USER/.rvm/scripts/rvm"  # This loads RVM into a shell session.
```
