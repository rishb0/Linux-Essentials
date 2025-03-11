# YUM Configuration on CentOS 9

YUM (Yellowdog Updater, Modified) is a powerful package management tool used in RPM-based Linux distributions like CentOS, RHEL, and Fedora. It simplifies the process of installing, updating, and managing software packages by handling dependencies and accessing remote repositories.

## Key Features of YUM

- **Automatic Dependency Resolution**: Automatically installs required dependencies for packages.
- **Remote Repository Support**: Downloads and installs packages from configured repositories.
- **Group Package Management**: Installs related packages grouped together (e.g., `Development Tools`).
- **Rollback Feature**: Allows undoing updates and reverting to previous package versions (in some versions).

**Note**: In modern Linux distributions, YUM has been replaced by DNF (Dandified YUM), which offers improved performance and better dependency handling. However, YUM is still widely used and understood.

---

## Configuring YUM with a Local Repository

In environments without internet access or with limited bandwidth, configuring YUM to use a local repository from a CentOS 9 ISO image is invaluable. This setup allows you to install and manage packages offline.

### Step 1: Mount the CentOS 9 ISO

Mount the CentOS 9 ISO image to access its contents. Assuming the ISO is available as a device (e.g., `/dev/sr0`):

```
mount /dev/sr0 /mnt/
```

### Step 2: Verify the Mount and Available Space

Check that the ISO is mounted correctly and verify available disk space:

```
df -h
```

### Step 3: Copy ISO Contents to a Directory

Create a directory to hold the ISO contents and copy them:

```
mkdir /centos9
```

```
cp -vr /mnt/* /centos9/
```

- `cp -vr`:
  - `-v`: Verbose output, shows files being copied.
  - `-r`: Recursively copy all files and directories.

### Step 4: Unmount the ISO

After copying the contents, unmount the ISO:

```
umount /mnt/
```

---

## Understanding the Repository Contents

Inside `/centos9`, you'll find several directories. Notably:

- **AppStream**: Contains additional software packages and modules not part of the minimal base OS but available for installation.
- **BaseOS**: Contains core packages required for the base operating system.

To see the number of packages in the `AppStream/Packages` directory:

```
ls -l /centos9/AppStream/Packages | wc -l
```

---

## Creating Repository Metadata with `createrepo`

YUM requires metadata to understand the packages available in a repository. We use `createrepo` to generate this metadata.

### Step 1: Install `createrepo`

Since we are working offline, we'll install `createrepo` from the packages we copied.

Find the `createrepo_c` packages:

```
ls /centos9/AppStream/Packages | grep createrepo_c
```

You should see:

```
createrepo_c-0.20.1-2.el9.x86_64.rpm
createrepo_c-libs-0.20.1-2.el9.x86_64.rpm
```

Install `createrepo_c` and its dependency `createrepo_c-libs` using `rpm`:

```
rpm -ivh /centos9/AppStream/Packages/createrepo_c-libs-0.20.1-2.el9.x86_64.rpm
```

```
rpm -ivh /centos9/AppStream/Packages/createrepo_c-0.20.1-2.el9.x86_64.rpm
```

- `rpm -ivh`:
  - `-i`: Install package.
  - `-v`: Verbose output.
  - `-h`: Display hash marks to show progress.

### Step 2: Verify `createrepo` Installation

Check the version of `createrepo` to verify it's installed:

```
createrepo -V
```

### Step 3: Generate Repository Metadata

Create the repository metadata for the packages in `AppStream/Packages`:

```
createrepo -vd /centos9/AppStream/Packages
```

- Options:
  - `-v`: Verbose output.
  - `-d` or `--database`: Create SQLite database files (used by YUM).

This command generates a `repodata` directory inside `/centos9/AppStream/Packages`, containing metadata files like `repomd.xml`, which YUM uses to resolve dependencies.

---

## Configuring YUM to Use the Local Repository

### Step 1: Backup Existing YUM Repository Files

Navigate to the YUM repository directory:

```
cd /etc/yum.repos.d
```

Create a backup directory and move existing repository files:

```
mkdir /backuprepo
```

```
mv /etc/yum.repos.d/* /backuprepo/
```

**Reason**: This prevents YUM from attempting to access online repositories, which is important for offline setups.

### Step 2: Verify No Repositories Are Enabled

Check the current list of repositories:

```
yum repolist all
```

You should see that no repositories are enabled.

### Step 3: Create a New YUM Repository Configuration File

Create a new repository file:

```
vim /etc/yum.repos.d/my-centos9.repo
```

Insert the following content:

```
[centos9]
name=CentOS 9 Local Repository
baseurl=file:///centos9/AppStream/Packages
enabled=1
gpgcheck=0
```

- **Explanation**:
  - `[centos9]`: Unique repository ID.
  - `name`: Descriptive name of the repository.
  - `baseurl`: Path to the local repository (note the three slashes).
  - `enabled=1`: Enables the repository.
  - `gpgcheck=0`: Disables GPG signature checking (since packages are from a trusted source).

**Optional**: Add the BaseOS repository:

```
[centos9-baseos]
name=CentOS 9 BaseOS Local Repository
baseurl=file:///centos9/BaseOS/Packages
enabled=1
gpgcheck=0
```

### Step 4: Clean YUM Cache and Rebuild Metadata

Clean all YUM caches:

```
yum clean all
```

Rebuild YUM cache:

```
yum makecache
```

### Step 5: Verify the New Repository

List all repositories to confirm your local repository is recognized:

```
yum repolist all
```

You should see entries for `centos9` and `centos9-baseos`.

### Step 6: List Available Packages

List all available packages from the repository:

```
yum list all
```

Or list only available (not installed) packages:

```
yum list available
```

---

## Installing Packages from the Local Repository

### Step 1: Search for a Package

To search for a specific package, use `yum search`:

```
yum search firefox
```

### Step 2: Install a Package

Install a package using `yum install` followed by the package name:

```
yum install firefox
```

YUM will resolve dependencies and install `firefox` along with any required packages from your local repository.

---

## Important Notes

- **Dependency Resolution**: By creating the repository metadata with `createrepo`, YUM can handle dependencies automatically, even in an offline environment.
- **GPG Check**: Setting `gpgcheck=0` disables GPG signature verification. Since you are using packages directly from the CentOS ISO (a trusted source), this is acceptable. In production environments with internet access, it's recommended to enable GPG checks.
- **Consistency**: Ensure that both `AppStream` and `BaseOS` repositories are configured if you want full access to all packages available on the CentOS 9 ISO.

---

## Troubleshooting Tips

- **Missing Packages**: If a package is not found, verify that it exists in your repository by listing contents:

  ```
  ls /centos9/AppStream/Packages | grep package-name
  ```

- **Dependency Errors**: If you encounter dependency issues, make sure that the repository metadata is up to date and that all necessary packages are available in your repository directories.

- **YUM Cache Issues**: If packages aren't being found or repositories aren't recognized, clean the YUM cache:

  ```
  yum clean all
  ```

  And rebuild the cache:

  ```
  yum makecache
  ```
