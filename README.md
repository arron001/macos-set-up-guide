# MacOS Set-up Guide

## Automated setting of custom macOS preferences

First off, get your new mac working in the way you're used to using it.

### Customise Dock appearance, behaviour & location

```
#Have the Dock show only active apps
defaults write com.apple.dock static-only -bool true

# Set dock size
defaults write com.apple.dock largesize -int 256

# Disable dots on apps
defaults write com.apple.dock show-process-indicators -bool false

# Disable recents
defaults write com.apple.dock show-recents -bool false

# Set dock to autohide
defaults write com.apple.dock autohide -bool true

# Set on right side
defaults write com.apple.dock orientation right

# Remember to run this after changing settings
killall Dock
``` 

---

### Customise Misc Settings
```
# Disable press-and-hold for keys in favor of key repeat.
defaults write -g ApplePressAndHoldEnabled -bool false

# Set a fast key repeat.
defaults write NSGlobalDomain KeyRepeat -int 1

# Show Safari's bookmark bar.
defaults write com.apple.Safari ShowFavoritesBar -bool true

# Set up Safari for development.
defaults write com.apple.Safari IncludeInternalDebugMenu -bool true

defaults write com.apple.Safari IncludeDevelopMenu -bool true

defaults write com.apple.Safari WebKitDeveloperExtrasEnabledPreferenceKey -bool true

defaults write com.apple.Safari "com.apple.Safari.ContentPageGroupIdentifier.WebKit2DeveloperExtrasEnabled" -bool true

defaults write NSGlobalDomain WebKitDeveloperExtras -bool true
```
---

### Finder:
```
# Set the Finder prefs for showing a few different volumes on the Desktop.
defaults write com.apple.finder ShowExternalHardDrivesOnDesktop -bool true

defaults write com.apple.finder ShowRemovableMediaOnDesktop -bool true

defaults write com.apple.finder ShowHardDrivesOnDesktop -bool true

defaults write com.apple.finder ShowMountedServersOnDesktop -bool true

# Adding ‘Quit’ option to Finder on a Mac
defaults write com.apple.finder QuitMenuItem -bool true

## Enable the expand save panel by default
defaults write NSGlobalDomain NSNavPanelExpandedStateForSaveMode -bool true

defaults write NSGlobalDomain NSNavPanelExpandedStateForSaveMode2 -bool true

# Display the file extensions in Finder
defaults write NSGlobalDomain AppleShowAllExtensions -bool true

# New window opens to home
defaults write com.apple.finder NewWindowTarget PfHm

# Don't use tabs
defaults write com.apple.finder FinderSpawnTab -bool false

# Don't show tags
defaults write com.apple.finder ShowRecentTags -bool false

# Don't warn when deleting files
defaults write com.apple.finder WarnOnEmptyTrash -bool false
defaults write com.apple.finder FXEnableRemoveFromICloudDriveWarning -bool false

# Empty bin after 30 days
defaults write com.apple.finder FXRemoveOldTrashItems -bool true

# Show Path Bar
defaults write com.apple.finder ShowPathbar -bool true

# Don't warn when changing file extensions
defaults write com.apple.finder FXEnableExtensionChangeWarning -bool false

# Set finder seach scope to current folder
defaults write com.apple.finder FXDefaultSearchScope SCcf

# Always open everything in Finder's list view.
defaults write com.apple.Finder FXPreferredViewStyle Nlsv

# Remember to run this after changing settings
killall Finder
```
If you want to add to the list above, follow this steps to find the domain & key responsible for a setting do this:

- Save the state before a change.

  `defaults read > before`

- Make change via GUI
- Save the state after a change.

  `defaults read > after`
- Find the domain & key responsible by viewing the diff

  `diff before after`

### Manual Customisations 
I haven't found the domain & key for these yet

- [ ] Set up three finger drag
  - Sys Pref > Accessibility > Pointer Control > Trackpad Options

- [ ] Set up scroll to zoom
  - Sys Pref > Accessibility > Zoom

- [ ] Turnoff autocorrect/auto-capitalise
  - System Pref. > Keyboard > Text

- [ ] Double check iCloud Settings, are you syncing everything you want? 
  - System Pref. > Apple ID

---
## Install Apps

- [ ] Install Homebrew: https://brew.sh
- [ ] Install Xcode from App Store / Xcodes

### Install apps via Homebrew:

- [ ] Download & Customise [Brew Packages.txt](Brew%20Packages.txt)
  - Tip you can find the packages installed on your old machine by running `brew list`
- [ ] Install all by running `brew install $(cat ~/Downloads/Brew\ Packages.txt)`
- [ ] After all installs are complete, review terminal logs for any additional package specific set-up 

---

## Set Git Credentials
- [ ] `git config --global user.email "{git account email address}"`
- [ ] `git config --global user.name "Your Name"`
- [ ] Set Atom as you custom editor for Git
  - `git config --global core.editor "/Applications/Atom.app/Contents/Resources/app/atom.sh -n -w"`
- [ ] Add these aliases to your <~/.gitconfig> file
```
[alias]
      st = status
      ci = commit
      br = branch
      co = checkout
      df = diff
      dt = difftool
      dr = !sh -c 'ref="$(git symbolic-ref --short HEAD)" && git df origin/$ref..$ref'
      dc = diff --cached
      lol = log --graph --decorate --pretty=oneline --abbrev-commit
      lola = log --graph --decorate --pretty=oneline --abbrev-commit --all
      ls = ls-files
```
        
## Set-up Terminal
- [ ] Install oh my zsh - https://ohmyz.sh/#install

Install ZSH Plugins:
- [ ] zsh-autosuggestions
https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md
- [ ] zsh-syntax-highlighting
https://github.com/zsh-users/zsh-syntax-highlighting/blob/master/INSTALL.md
- [ ] Add plugins to .zshrc file: 
```
plugins=(git zsh-autosuggestions zsh-syntax-highlighting)
```
- [ ] If not working, double check you copied the plugins to the correct dir `~/.oh-my-zsh/custom/plugins`
---

## Configure Apps

- [ ] Restore files from Cloud/HD back-ups

- [ ] Link Music & Photos Apps to restored libraries 
  - Option + Open Photos / Music > then select your restored library

- [ ] Restore IntelliJ Settings from Git Repo / Previous Mac back-up

- [ ] Install command line launcher for IntelliJ
  - IntelliJ > Tools > Create Command-line Launcher...

- [ ] Restore FlyCut preferences from iCloud

- [ ] Restore iTerm2 preferences from back-up file
  - [This pref file](com.googlecode.iterm2.plist) sets-up iTerm2 with:
    - a translucent dropdown terminal that supports tabs. 
    - Support for common navigation shortcuts 
      - Option + Left/Right Arrow to skip a word
      - CMD + Left/Right Arrow to skip to front/back of current line
    - Note: You will want to change the working directory path on line 854 of the pref file before loading.
  - Open iTerm2, and then show / hide the terminal with keyboard shortcut Option + Space bar

- [ ] Set chosen apps to open at login
  - iTerm2
  - FlyCut
  - Anything else your heart desires

---
