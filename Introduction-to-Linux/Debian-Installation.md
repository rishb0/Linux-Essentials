# Installing Debian on VirtualBox

Welcome to this detailed guide on installing Debian on VirtualBox. This guide will walk you through downloading the Debian ISO, creating and configuring a new virtual machine, partitioning the disk, and completing the installation—all with theory and screenshots to help you every step of the way.

---

## 1. Download Required Files

- **Download Debian ISO**  
  Visit the official [Debian Download](https://www.debian.org/download) page and download the ISO file.
  
  ![Download Debian ISO](https://github.com/user-attachments/assets/6bea27d5-8055-4eda-9fbb-487437b9a695)

---

## 2. Create a New Virtual Machine (VM)

1. Open VirtualBox and click **New**.
2. Enter the following details:
   - **Name**: Debian
   - **Type**: Linux
   - **Version**: Debian (64-bit)
3. Select Debian ISO
4. Click **Next**.

![image](https://github.com/user-attachments/assets/6f950f1c-8cf5-459b-b584-24b783c97580)

![image](https://github.com/user-attachments/assets/d8fd51ca-26cd-4d02-836a-b8664e9b90bc)

---

## 3. Configure Virtual Machine Settings

### A. Allocate RAM
- **Recommended**: At least **2048 MB (2 GB)**.
- For better performance (especially with a desktop environment), you can assign **4096 MB (4 GB)** if your host hardware permits.

### B. Create a Virtual Hard Disk
1. Select **"Create a virtual hard disk now"** and click **Create**.
2. Choose **"VDI (VirtualBox Disk Image)"** and click **Next**.
3. Set **Storage on physical hard disk** to **"Dynamically allocated"**.
4. Set the disk size – **Recommended**: 40 GB or more.
5. Click **Create**.

![image](https://github.com/user-attachments/assets/3e95d2e6-75c4-4bc4-aeae-e8510ef3e778)

![image](https://github.com/user-attachments/assets/d7d7199f-f523-4f34-87bc-2217cf12fa66)

---

## 4. Start Debian Installation

1. Click **Start** to boot the VM.
2. When presented with the boot menu, choose either **"Graphical Install"** (recommended for ease of use) or **"Install"** (text-based installer).

![image](https://github.com/user-attachments/assets/86e1d4bc-a72c-4544-82fd-be05279fa611)

---

## 5. Select Language, Location, and Keyboard

- **Language**: Choose your preferred language.

  ![image](https://github.com/user-attachments/assets/84eb9cd0-3489-4589-906f-a6f0b2b576ac)

- **Location**: Select your country.

  ![image](https://github.com/user-attachments/assets/c0021135-207e-4c92-a868-bafd27fdf4fd)

- **Keyboard**: Choose your keyboard layout (default is usually US; select another if required).

  ![image](https://github.com/user-attachments/assets/2158579a-79a0-4a89-a60e-23f87e4a1987)

These selections help configure locale settings such as date formats and language options.

---

## 6. Configure Network

- Set a **hostname** for your system—for example, `debian`.

  ![image](https://github.com/user-attachments/assets/df510ef2-f48d-49ba-b052-eadccfbee2c6)

- Enter a **domain name** if needed, or you can leave it empty.

  ![image](https://github.com/user-attachments/assets/c2a015b4-de8b-475f-a14c-5bcc5815235f)

---

## 7. Set Root Password

- You will be asked to create a strong password for the root account (which has full privileges).

  ![image](https://github.com/user-attachments/assets/b3fae84c-ea91-48e4-8503-cc3854ac1fd6)

---

## 8. Create User and Set Passwords

- **Create a New User**:  
  - Fill in the full name, username, and password for the non-root account.  

  ![image](https://github.com/user-attachments/assets/c29e7e9c-9a3c-491d-940e-d0afc8973e50)

  ![image](https://github.com/user-attachments/assets/334e8a09-7c15-43b4-9527-62f5d2fa28c5)

  ![image](https://github.com/user-attachments/assets/18686a14-6139-46d3-952c-ea654f8f08ae)

- Using a non-root account for daily tasks increases system security.

---

## 9. Partition the Disk – (Manual Partitioning Method)

When you reach the partitioning step, you have options:

1. **Guided Options**:  
   - Use entire disk
   - Use entire disk with LVM
   - Use entire disk with encrypted LVM

### Theory & Key Points – Partitioning Options
- **Guided partitioning** simplifies the setup by automating partition creation.
- **Manual partitioning** offers flexibility for custom layouts (for example, splitting /home, /var, etc.).
- **LVM (Logical Volume Manager)** provides flexible storage management.
- **Encryption** options add an extra security layer for your data.

2. **Manual Partitioning**: Gives full control over partition setup. This guide demonstrates the manual method for a 40 GB disk.

### Recommended Partition Scheme:

![image](https://github.com/user-attachments/assets/39c5ae80-42df-40ef-8df3-3b848bf492e9)

- Select hard disk 

  ![image](https://github.com/user-attachments/assets/c7197454-00fe-4165-8a32-8573da7feea9)

  ![image](https://github.com/user-attachments/assets/e656ebe4-b142-4e0e-a2b1-c77a8a74e6b3)

#### A. Boot Partition
- **Mount Point**: `/boot`
- **Size**: 2 GB (stores bootloader files and kernel images)
- **Type**: Primary
- **Filesystem**: ext4

  ![image](https://github.com/user-attachments/assets/31a74d63-9c09-4d51-8b12-584cf9db4815)

  ![image](https://github.com/user-attachments/assets/623a06bb-e347-4e6d-9916-a44ac6644725)

  ![image](https://github.com/user-attachments/assets/5e81c191-bff2-4c52-b7a1-6e0baad6e100)

  ![image](https://github.com/user-attachments/assets/54c92c64-f790-4b40-9bbe-6c6dfdfd2530)

  ![image](https://github.com/user-attachments/assets/765a53d8-0314-4852-958b-1abba92bbbcc)

  ![image](https://github.com/user-attachments/assets/18dce863-71c4-486b-a50a-007bc47f2b0c)

#### B. Swap Partition
- **Size**: 2 GB (or around the size of your physical RAM; typically do not exceed 4 GB in a VM)
- **Type**: Logical
- **Use as**: Swap area

  ![image](https://github.com/user-attachments/assets/e16e75a7-d3cb-48d1-bdb3-079716576669)

  ![image](https://github.com/user-attachments/assets/82ca7759-f43c-439a-82da-2cb9ded05811)

  ![image](https://github.com/user-attachments/assets/fec6918e-1379-4a68-9ba9-f046ca8fedd3)

  ![image](https://github.com/user-attachments/assets/a6dc8ce3-b6ea-4377-bea9-54c7c85b02c9)

  ![image](https://github.com/user-attachments/assets/bcf91736-2947-4016-9b08-ded2aaf80f32)

  ![image](https://github.com/user-attachments/assets/492dc8bb-2399-4f80-b4af-4b3e6214e6ac)

  ![image](https://github.com/user-attachments/assets/f43f0eff-35bd-407a-92ee-13a8a97e5a6b)

  ![image](https://github.com/user-attachments/assets/8bed231f-54a4-4484-8014-e56e93b5d956)

#### C. Root Partition
- **Mount Point**: `/`
- **Size**: Remaining space on the disk
- **Type**: Primary
- **Filesystem**: ext4

  ![image](https://github.com/user-attachments/assets/36cca7b9-1909-4824-91a0-b037c9ccd5be)

  ![image](https://github.com/user-attachments/assets/1a55f95b-68d6-4dec-acf7-82dd5ad496ac)

  ![image](https://github.com/user-attachments/assets/7f3d1257-ffcf-46d4-ad22-89853b8d6d8c)

  ![image](https://github.com/user-attachments/assets/2a75c7d8-9169-438d-9abb-402dd3403844)

  ![image](https://github.com/user-attachments/assets/cae1edb9-3177-4ae7-99e4-8eb88445c38d)

#### D. Finish Partitioning

- Note: This will write changes to the disk, ensure everything is correct.

  ![image](https://github.com/user-attachments/assets/954b1447-3865-4215-a3a6-9c1e210cc5ba)

  ![image](https://github.com/user-attachments/assets/2d20a3cc-94fa-4227-adaa-5894c3ef1c14)

---

## 10. Install the Base System

- The installer will now copy the base system files onto the disk.
- This process may take several minutes; please be patient.

  ![image](https://github.com/user-attachments/assets/705af77a-4154-4472-bcdd-aa03a15dfaee)

---

## 11. Configure Package Manager Source

- By default, Debian uses online repositories to install packages.
- Click **No** if you do not want to install packages from local installation media.
- For new users, it is recommended to **Click No**.

  ![image](https://github.com/user-attachments/assets/8c7d9fcf-9700-4c92-aa88-fb7dda573922)

---

## 12. Configure Mirrors for Package Installation

- Select your country or continent.

  ![image](https://github.com/user-attachments/assets/0956d203-e652-4503-880b-e321afebe093)

- Select the Debian archive mirror.
- It is recommended to go with `deb.debian.org`.

  ![image](https://github.com/user-attachments/assets/9f1a397a-7748-490c-becf-f757aeb0e2b9)

---

## 13. Configure Proxy Server

- For beginners, skip this step and leave it blank.

  ![image](https://github.com/user-attachments/assets/f320f5fc-964b-4a9b-8077-587f06468578)

---

## 14. Configure Package Usage Survey Participation

- This option allows Debian to anonymously collect data on the most used packages, aiding developers in optimizing package selections.
- It is recommended to select **No** to maintain privacy, but you can opt-in if you wish to contribute usage statistics.

  ![image](https://github.com/user-attachments/assets/3b48c5a9-464f-45f6-ab6a-afd89f8502cc)

---

## 15. Select Software

- **Desktop Environment**: Choose from available options such as GNOME (default), KDE, XFCE, LXDE, Cinnamon, etc.
- **Standard System Utilities**: Recommended for essential system management tools.
- **SSH Server**: Optionally select this if you plan to access your Debian VM remotely.

  ![image](https://github.com/user-attachments/assets/157a5c86-4403-4fa8-a02e-07a8872a8521)

Choose your software selections and continue with the installation process.

---

## 16. Install GRUB Bootloader

- When prompted, choose **Yes** to install the GRUB bootloader.
- GRUB will allow you to boot into Debian (and any other operating systems if applicable).

  ![image](https://github.com/user-attachments/assets/535f3365-292f-499a-87a3-806176ba64df)

  ![image](https://github.com/user-attachments/assets/0449fb56-6259-4387-aea7-6b182c0ae279)

---

## 17. Finish Installation & Reboot

- After all installation steps are complete, the installer will prompt you to reboot.
- Remove the ISO from your virtual machine’s storage settings if necessary.

- Boot Normally

  ![image](https://github.com/user-attachments/assets/19e7c795-bd91-4003-aa47-34b7602dd828)

---

# Congratulations!

You have now successfully installed Debian on VirtualBox. This guide covered everything from downloading the ISO file, creating and configuring the VM, partitioning the disk manually, selecting software, and installing the GRUB bootloader.
