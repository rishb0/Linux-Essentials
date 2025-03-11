# Shells in Linux

In Linux, a shell is a command-line interface (CLI) that allows users to interact with the operating system. It serves as a bridge between the user and the kernel, interpreting and executing user commands, scripts, and automation workflows. Shells are an integral part of the Linux ecosystem, enabling a flexible and powerful environment for system management, development, and more.

---

### What is a Shell?

A shell is a program that processes commands and returns the output. It provides a text-based interface for users to:

- Execute commands to interact with the operating system.
- Automate tasks using scripts.
- Access system resources and utilities.

### Types of Shells

Shells in Linux can be broadly categorized into two types:

- **Login Shells**: Started when a user logs in via a terminal, displaying a login prompt.
- **Interactive Shells**: Used after logging in, allowing users to type and execute commands.

---

### Common Shells in Linux

#### 1. **sh (Bourne Shell)**

**Overview**: The original Unix shell developed by Stephen Bourne.

**Features**:

- Focuses on executing commands and writing simple scripts.
- Supports variables, loops, conditionals, and redirection.
- Limited interactive features compared to modern shells.

**Advantages**:

- Lightweight and highly compatible with POSIX standards.
- Useful for running basic scripts across various Unix-like systems.

**Disadvantages**:

- Lacks advanced features like command history or tab completion.

**Use Case**: Legacy systems and simple shell scripts.

---

#### 2. **bash (Bourne Again Shell)**

**Overview**: An improved version of the Bourne shell, created for GNU/Linux.

**Features**:

- Combines sh compatibility with modern enhancements.
- Includes features like:
  - Command history.
  - Tab completion.
  - Script debugging with set options (`set -x`, `set -e`).
  - Aliases and functions.

**Advantages**:

- Default shell in most Linux distributions.
- Extensive scripting capabilities.
- Large community and documentation support.

**Disadvantages**:

- Heavier than some alternatives like dash.

**Use Case**: General-purpose shell for users, administrators, and developers.

---

#### 3. **ksh (Korn Shell)**

**Overview**: Combines the features of sh and csh, developed by David Korn.

**Features**:

- Powerful scripting capabilities with advanced data structures (e.g., associative arrays).
- High performance in computational tasks.
- Command-line editing and history manipulation.

**Advantages**:

- Suitable for complex scripting and performance-critical tasks.
- Includes floating-point arithmetic and job control.

**Disadvantages**:

- Less commonly used, leading to limited community support.

**Use Case**: Programming environments and advanced automation.

---

#### 4. **tcsh (TENEX C Shell)**

**Overview**: An enhanced version of the original C shell (csh), incorporating features from TENEX.

**Features**:

- Command-line editing with Emacs and Vi-like bindings.
- Spelling correction and auto-completion.
- Extended scripting support compared to csh.

**Advantages**:

- User-friendly for interactive sessions.
- Syntax familiarity for users of csh.

**Disadvantages**:

- Non-POSIX compliant; scripting is less portable.

**Use Case**: Interactive command-line use and environments preferring csh syntax.

---

#### 5. **fish (Friendly Interactive Shell)**

**Overview**: A modern shell emphasizing ease of use and interactivity.

**Features**:

- Syntax highlighting and autosuggestions.
- Built-in help for commands (fish includes a comprehensive help system).
- Smart tab completion and history search.
- User-friendly design without requiring extensive configuration.

**Advantages**:

- Intuitive interface, ideal for beginners.
- Provides a rich out-of-the-box experience.

**Disadvantages**:

- Not fully compatible with POSIX standards, limiting script portability.

**Use Case**: Users prioritizing ease of use and interactive features.

---

#### 6. **zsh (Z Shell)**

**Overview**: A highly customizable shell that is compatible with bash and offers extended functionality.

**Features**:

- Shared command history between sessions.
- Spell-checking and globbing capabilities.
- Frameworks like Oh My Zsh enable plugins and themes for customization.
- Advanced features like recursive globbing and autocorrection.

**Advantages**:

- Combines the best features of bash, tcsh, and ksh.
- Highly extensible for productivity enthusiasts.

**Disadvantages**:

- Configuration can be complex for new users.

**Use Case**: Advanced users and developers seeking customization and productivity.

---

#### 7. **dash (Debian Almquist Shell)**

**Overview**: A lightweight shell optimized for scripting, often used as `/bin/sh`.

**Features**:

- Minimal resource consumption.
- Compliant with POSIX standards, ensuring script portability.
- Ideal for embedded systems and small environments.

**Advantages**:

- Fast and efficient for scripting tasks.
- Used in critical system environments like init scripts.

**Disadvantages**:

- Lacks advanced interactive features.

**Use Case**: System scripts, embedded systems, and environments requiring speed and compliance.

---

### Which Shell Should You Use?

The choice of shell depends on your specific needs:

- For **scripting and compatibility**: sh or bash.
- For **performance-critical tasks**: ksh or dash.
- For **interactive and user-friendly environments**: fish or zsh.
- For **legacy systems**: sh or tcsh.

---

### How to Change the Default Shell

You can change the default shell for your user account using the `chsh` command:

**View available shells**:

```
cat /etc/shells
```

**Change the shell**:

```
chsh -s /bin/bash  # Replace /bin/bash with your desired shell.
```

---

### Shell Variables and `$SHELL`

#### What is `$SHELL`?

`$SHELL` is an environment variable in Linux that holds the path to the default shell for the current user. It indicates which shell is set for the user account as their default shell, typically configured in `/etc/passwd`.

#### How to View the Current Default Shell?

You can display the value of the `$SHELL` variable using the `echo` command:

```
echo $SHELL
```

This will output the path to the user's default shell, such as:

```
/bin/bash
```

#### When is `$SHELL` Initialized?

`$SHELL` is initialized when the operating system boots and a user logs into their account. The default shell specified in `/etc/passwd` for the user determines the initial value of `$SHELL`.

**Example entry in `/etc/passwd`**:

```
username:x:1000:1000:User Name:/home/username:/bin/bash
```

---

### Changing the Shell Temporarily

You can invoke a different shell by typing its name (e.g., `sh`, `bash`, `zsh`) in the terminal.

**Example**:

```
sh    # Switches to the Bourne shell
```
```
bash  # Switches to the Bash shell
```

**What Happens?**

- A new shell instance is created as a subprocess of the current shell.
- The parent shell remains active in the background, and the `$SHELL` variable does not change.
- You can exit the new shell instance by typing `exit` or pressing `Ctrl+D`, returning to the parent shell.

---

### Changing the Default Shell Permanently

To permanently change the default shell, use the `chsh` command:

**View available shells**:

```
cat /etc/shells
```

**Change the default shell**:

```
chsh -s /bin/zsh  # Replace /bin/zsh with the desired shell path
```

- **Note**: Log out and log back in for the changes to take effect.

---

### How to Verify the Current Shell

You can verify the active shell by running the following command:

```
echo $0
```

This will display the name of the currently active shell. For example:

- If you're in `sh`, it might return `sh`.
- If you're in `bash`, it might return `bash`.

