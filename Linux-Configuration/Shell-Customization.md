# Installation of Zsh  
Zsh is a powerful shell with advanced features like syntax highlighting, autosuggestions, and themes.  

## Install Zsh  
- Install Zsh and its addons:  

```
yum install zsh*
```  

## Check Installation  
- Verify the version and location:  

```
zsh --version
```
```
which zsh
```  

## Configure Zsh  

### 1. Set Up Configuration  
- Use a `.zshrc` file to customize Zsh. For example, copy the `.zshrc` file from Kali Linux to make Zsh look similar.  

### 2. Set Zsh as the Default Shell  
- Find the location of Zsh:  

```
which zsh
```  

- Set it as the default shell:  

```
chsh -s $(which zsh)
```  

### What Happens?  
This changes your default shell in the `/etc/passwd` file, which stores user account information, including the default shell.  

## Features of Zsh  
- **Themes**: Customize the prompt and appearance.  
- **Plugins**: Install plugins like oh-my-zsh for additional features.  
- **Auto-completion**: Provides advanced completion for commands.  

---

# Increasing the Power of a Shell  
A shell can be made more powerful and user-friendly by adding plugins and utilities that enhance its capabilities. These improvements can include:  

1. Auto-completion for commands and file paths.  
2. Colorized output for better readability.  
3. Aliases to shorten or simplify frequently used commands.  
4. Enhanced customization through configuration files.  

## Shell Plugins (Add-ons)  
Plugins or add-ons are additional features or tools that enhance the functionality of a shell. For example:  
- **Bash plugins** can add auto-completion, colored prompts, and more.  
- **Tools like grc** add color to the output of commands, improving visual clarity.  

---

# Installing Shell Plugins  

## 1. Installing Plugins for Bash  
- Command:  

```
yum install bash*
```  

The `*` wildcard ensures that all packages related to "bash" are installed.  

## 2. Search for Specific Plugins  
- Command:  

```
yum search bash
```  

This lists all available packages related to "bash."  

## 3. Install Specific Plugins  
- **Auto-completion plugin**:  

```
yum install bash-completion.noarch
```  

After installation, typing part of a command and pressing `Tab` completes the command automatically.  

- **Color prompt plugin**:  

```
yum install bash-color-prompt.noarch
```  

This changes the terminal prompt to a colored format for better visibility.  

## 4. Verify Plugins  
- After installing a plugin, exit the session and re-login to see the changes.  
- For example, try using `Tab` completion after installing `bash-completion.`  

---

# Making the Terminal Colorful with grc  
The `grc` tool is used to add color to the output of certain commands.  

## Installing grc  

### 1. Download grc  
- If `wget` is not installed, install it first:  

```
yum install wget
```  

- Download the `grc` package from GitHub:  

```
wget https://github.com/garabik/grc/archive/refs/tags/v1.13.tar.gz
```  

### 2. Extract the Package  
- Extract the tar file:  

```
tar -xvf v1.13.tar.gz
```  

### 3. Move to `/opt/` Directory  
- Move the extracted folder (`grc-1.13`) to `/opt/`:  

```
mv grc-1.13 /opt/
```  

### Why `/opt/`?  
`/opt/` is used for installing optional or third-party software that isn't part of the default system.  

### 4. Install grc  
- Navigate to the directory and run the installer script:  

```
cd /opt/grc-1.13
./install.sh
```  

### 5. Test grc  
- Try using `grc` with supported commands:  

```
grc ping 8.8.8.8
grc ifconfig
```  

- For unsupported commands, `grc` won’t add color. You can check the supported commands in the `grc.sh` file on GitHub.  

---

# Aliases with grc  
- The file contains lines like this:  

```
alias blkid='colourify blkid'
```  

### Explanation:  
The `colourify` function is a wrapper that applies `grc` automatically to the specified command (e.g., `blkid`). By setting these aliases, you don’t need to prepend `grc` manually.  

---

# Persistent Configuration  

## 1. Add Aliases to `.bashrc`  
- Place aliases in the `.bashrc` file:  

```
alias ping='grc ping'
```  

- Reload the `.bashrc` file without restarting:  

```
source /root/.bashrc
```  

## 2. Automate with `grc.sh`  
- Copy the `grc.sh` script to `/etc/`:  

```
cp /opt/grc-1.13/grc.sh /etc/
```  

- Add this to `.bashrc`:  

```
GRC_ALIASES=true
[[ -s "/etc/profile.d/grc.sh" ]] && source /etc/grc.sh
```  

---

# Summary of Key Concepts  

| Feature/Command        | Explanation                                        |  
|------------------------|----------------------------------------------------|  
| `sh`, `bash`          | Temporarily start a new shell session.             |  
| `$SHELL`              | Shows the default shell for the user.               |  
| `.bashrc`             | Configuration file for bash at login.               |  
| `grc`                 | Adds color to command output.                       |  
| `zsh`                 | A feature-rich shell with plugins and themes.       |  
| `chsh -s $(which zsh)` | Permanently change the default shell.               |  

