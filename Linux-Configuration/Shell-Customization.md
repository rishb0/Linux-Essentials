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
## Features of Zsh  
- **Themes**: Customize the prompt and appearance.  
- **Plugins**: Install plugins like oh-my-zsh for additional features.  
- **Auto-completion**: Provides advanced completion for commands.  


## Increasing the Power of a Shell  
A shell can be made more powerful and user-friendly by adding plugins and utilities that enhance its capabilities. These improvements can include:  

1. Auto-completion for commands and file paths.  
2. Colorized output for better readability.  
3. Aliases to shorten or simplify frequently used commands.  
4. Enhanced customization through configuration files.  

## Shell Plugins (Add-ons)  
Plugins or add-ons are additional features or tools that enhance the functionality of a shell. For example:  
- **Bash plugins** can add auto-completion, colored prompts, and more.  
- **Tools like grc** add color to the output of commands, improving visual clarity.  



## Installing Shell Plugins  

- The `*` wildcard ensures that all packages related to "bash" are installed.  

```
yum install bash*
```  

- This lists all available packages related to "bash."  

    ```
    yum search bash
    ```  
- **Auto-completion plugin**:  

    ```
    yum install bash-completion.noarch
    ```  

    After installation, typing part of a command and pressing `Tab` completes the command automatically.  

- **Color prompt plugin**:  

    ```
    yum install bash-color-prompt.noarch
    ```  
## Verify Plugins  
- After installing a plugin, exit the session and re-login to see the changes.  
- For example, try using `Tab` completion after installing `bash-completion.`  



## Making the Terminal Colorful with grc  
The `grc` tool is used to add color to the output of certain commands.  

### Installing grc  

- If `wget` is not installed, install it first:  

    ```
    yum install wget
    ```  

- Download the `grc` package from GitHub:  

    ```
    wget https://github.com/garabik/grc/archive/refs/tags/v1.13.tar.gz
    ```  

    - Extract the tar file:  

    ```
    tar -xvf v1.13.tar.gz
    ``` 
- Move the extracted folder (`grc-1.13`) to `/opt/`:  

    ```
    mv grc-1.13 /opt/
    ```  
- Navigate to the directory and run the installer script:  

    ```
    cd /opt/grc-1.13
    ./install.sh
    ```
- Try using `grc` with supported commands:  

    ```
    grc ping 8.8.8.8
    grc ifconfig
    ```  



# Aliases with grc  
- The file contains lines like this:  

```
alias blkid='colourify blkid'
```  



## Persistent Configuration  

### Add Aliases to `.bashrc`  
- Place aliases in the `.bashrc` file:  

    ```
    alias ping='grc ping'
    ```  

- Reload the `.bashrc` file without restarting:  

    ```
    source /root/.bashrc
    ```

### Automate with `grc.sh`
- Copy the `grc.sh` script to `/etc/`:

    ```
    cp /opt/grc-1.13/grc.sh /etc/
    ```

- Add this to `.bashrc`:

    ```
    GRC_ALIASES=true
    [[ -s "/etc/profile.d/grc.sh" ]] && source /etc/grc.sh
    ```