# Configuring Online YUM Repositories on CentOS 9

To manage software packages on CentOS 9, you can use the YUM (Yellowdog Updater, Modified) package manager. By ensuring that you have the necessary repositories configured, you gain access to a vast array of software packages and updates. This guide covers how to verify existing repositories and add additional ones to extend the capabilities of your system.

---

## Verifying Existing YUM Repositories

CentOS 9 comes with default YUM repositories that are crucial for system updates and base packages. To ensure these repositories are present:

1. **List All Repositories:**

   ```
   yum repolist all
   ```

   This command displays all repositories, including those that are enabled and disabled.

2. **Check the `/etc/yum.repos.d/` Directory:**

   Ensure that all default YUM repository configuration files are present in this directory.

---

## Understanding YUM Repository Configuration

YUM repositories are defined by configuration files located in `/etc/yum.repos.d/`. Each repository configuration includes several parameters:

| **Term**            | **Description**                                                      |
|---------------------|----------------------------------------------------------------------|
| `repo id`           | Unique identifier of the repository                                  |
| `name`              | Human-readable name of the repository                                |
| `baseurl`           | Direct URL to fetch RPM packages and metadata                        |
| `metalink`          | URL pointing to a file containing a list of mirrors                  |
| `gpgkey`            | Path or URL to the GPG key for verifying package authenticity        |
| `gpgcheck`          | Enables (`1`) or disables (`0`) GPG signature verification for packages |
| `repo_gpgcheck`     | Enables (`1`) or disables (`0`) GPG verification for repository metadata |
| `metadata_expire`   | Time before YUM refreshes repository metadata                        |
| `countme`           | Tracks repository usage statistics                                   |
| `enabled`           | Enables (`1`) or disables (`0`) the repository                       |

---

## Default CentOS 9 Repositories

The following are the official repositories included by default in CentOS 9:

1. **BaseOS**

   - Contains the core set of packages needed for a minimal operating system installation.
   - Essential for the system's basic functionality.

2. **AppStream**

   - Provides additional user-space applications, libraries, and development tools.
   - Allows users to install newer versions of software than those available in BaseOS.

3. **Extras**

   - Contains packages that provide additional functionality not included in BaseOS or AppStream.

These repositories should be present and enabled for your system to function correctly and receive updates.

---

## Adding Unofficial Online Repositories

To access a wider range of software packages, you can enable additional repositories. The most popular unofficial repositories for CentOS 9 are:

1. **EPEL (Extra Packages for Enterprise Linux)**
2. **REMI Repository**
3. **RPM Fusion Repository**
4. **ELRepo**

### Important Note:

- **IUS Repository**: The IUS (Inline with Upstream Stable) repository is only available up to CentOS 7 and does not support CentOS 9.

---

### 1. Enabling the EPEL Repository

**About EPEL:**

- Provides high-quality add-on packages that are not included in the default CentOS repositories.
- Maintained by the Fedora Special Interest Group.

**Installation Steps:**

1. **Install the EPEL Release Package:**

   ```
   rpm -ivh https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm
   ```

2. **Verify the Repository:**

   ```
   yum repolist
   ```

   **Expected Output:**

   - You should see `epel` and `epel-cisco-openh264` listed among the repositories.
   - Running `yum repolist all` will show both enabled and disabled repositories.

---

### 2. Enabling the REMI Repository

**About REMI:**

- Provides the latest versions of PHP, MySQL, and other related software packages.
- Ideal for users needing newer software versions than those available in the official repositories.

**Installation Steps:**

1. **Install the REMI Release Package:**

   ```
   rpm -ivh https://rpms.remirepo.net/enterprise/remi-release-9.rpm
   ```

2. **Verify the Repository:**

   ```
   yum repolist
   ```

   **Expected Output:**

   - You should see `remi-modular` and `remi-safe` listed among the repositories.
   - Running `yum repolist all` will show both enabled and disabled repositories.

---

### 3. Enabling the RPM Fusion Repository

**About RPM Fusion:**

- Offers additional packages not included in the official repositories, often due to licensing reasons.

**Installation Steps:**

1. **Install the RPM Fusion Free Repository:**

   ```
   rpm -ivh https://download1.rpmfusion.org/free/el/rpmfusion-free-release-9.noarch.rpm
   ```

2. **Verify the Repository:**

   ```
   yum repolist
   ```

   **Expected Output:**

   - You should see `rpmfusion-free-updates` listed among the repositories.

---

### 4. Enabling the ELRepo Repository

**About ELRepo:**

- Specializes in hardware-related packages, including file system drivers, graphics drivers, network drivers, and more.

**Installation Steps:**

1. **Import the GPG Keys:**

   ```
   rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
   ```

   ```
   rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
   ```

2. **Install the ELRepo Release Package:**

   ```
   rpm -ivh https://www.elrepo.org/elrepo-release-9.el9.elrepo.noarch.rpm
   ```

3. **Verify the Repository:**

   ```
   yum repolist
   ```

   **Expected Output:**

   - You should see `elrepo` listed among the repositories.

---

## Conclusion

By adding these four repositories—**EPEL**, **REMI**, **RPM Fusion**, and **ELRepo**—you significantly enhance your CentOS 9 system's capabilities. These repositories provide access to a wide range of additional packages and can help resolve dependencies that the default repositories might not cover.

**Note:**

- **All Dependencies Resolved:** With these repositories, most package dependencies should be resolved without needing any additional repositories.
- **Careful Usage:** While these repositories are reputable, adding multiple external repositories can sometimes lead to package conflicts. Always verify compatibility and consider enabling repositories only when needed.
