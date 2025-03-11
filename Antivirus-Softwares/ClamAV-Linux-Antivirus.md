

---

# ClamAV Installation and Usage on CentOS

This guide will walk you through the installation of **ClamAV** on CentOS, updating the virus database, using it for file and directory scans, and testing its functionality using the **EICAR test file**.

## Step 1: Install ClamAV on CentOS

1. **Enable the EPEL Repository**:
   Ensure that the **EPEL repository** is enabled, as ClamAV is often included in this repository:

   ```bash
   sudo yum install epel-release
   ```

2. **Install ClamAV**:
   After enabling the EPEL repository, install ClamAV using the following command:

   ```bash
   sudo yum install clamav*
   ```

---

## Step 2: Update ClamAV Database

ClamAV requires an updated virus definition database to work effectively. Run the following command to update it:

```bash
sudo freshclam
```

This will download the latest virus definitions to ensure ClamAV is up to date.

---

## Step 3: Verify ClamAV Installation

To check if ClamAV is installed and working correctly, you can run the following commands:

1. **Check ClamAV Version**:

   ```bash
   clamscan --version
   ```

   This should display the version of ClamAV installed.

2. **Scan a Directory or File**: To verify that ClamAV is working, run a scan on a specific directory or file:

   ```bash
   clamscan /path/to/your/file
   ```

   Or

   ```bash
   clamscan /path/to/your/directory
   ```

---

## Step 4: Using ClamAV for Scanning

Once ClamAV is installed and updated, you can use it to scan files or directories:

1. **Scan a Single File**:

   ```bash
   clamscan /path/to/your/file
   ```

2. **Scan a Directory**:

   ```bash
   clamscan /path/to/your/directory
   ```

   This command will output the results to the terminal by default.

---

## Step 5: Scan with Additional Options

ClamAV provides several options to customize your scans:

1. **Scan Recursively (for directories)**:

   ```bash
   clamscan -r /path/to/your/directory
   ```

2. **Show Detailed Output for Each File**:

   ```bash
   clamscan -v /path/to/your/file_or_directory
   ```

3. **Scan and Move Infected Files to Quarantine**:

   ```bash
   clamscan --move=/path/to/quarantine /path/to/your/file_or_directory
   ```

4. **Scan and Remove Infected Files**:

   ```bash
   clamscan --remove /path/to/your/file_or_directory
   ```

5. **Log Results to a File**:

   ```bash
   clamscan -l /path/to/logfile.txt /path/to/your/file_or_directory
   ```

---

## Step 6: Using ClamAV Daemon (clamd) for Faster Scanning

To scan files more efficiently, you can use the **ClamAV Daemon (clamd)**. This daemon keeps virus definitions in memory, providing faster scans.

1. **Scan with `clamdscan`**:

   ```bash
   clamdscan /path/to/your/file_or_directory
   ```

---

## Step 7: Schedule Regular Scans (Optional)

To automate ClamAV scans, you can use **cron jobs**. For example, to schedule a daily scan at 2 AM:

1. Edit the cron table:

   ```bash
   crontab -e
   ```

2. Add a line to run a scan every day at 2 AM:

   ```bash
   0 2 * * * clamscan -r /path/to/your/directory --log=/path/to/logfile.txt
   ```

---

## Step 8: Checking Logs

You can check ClamAV logs for additional details about scans and updates. By default, logs may be stored in `/var/log/clamav/`.

- **Check ClamAV Logs**:

   ```bash
   cat /var/log/clamav/clamd.log
   ```

---

## Step 9: Regularly Update ClamAV Definitions

To keep your virus definitions up to date, run the `freshclam` command periodically:

```bash
sudo freshclam
```

This ensures that your ClamAV virus definitions are always updated to the latest version.

---

## Step 10: Test ClamAV with EICAR Test File

You can test your ClamAV installation using the **EICAR Anti-Malware Test File**, which is specifically designed to trigger antivirus software without being a real virus.

### Download the EICAR Test File

You can download the EICAR test file from the following link:

[EICAR Anti-Malware Test File](https://www.eicar.org/download/eicar.com)

Alternatively, you can download it directly using `wget`:

```bash
wget https://www.eicar.org/download/eicar.com -O /path/to/your/directory/eicar.com
```

### Scan the EICAR Test File

After downloading the test file, you can run a scan to verify that ClamAV is working:

```bash
clamscan /path/to/your/directory/eicar.com
```

ClamAV should detect the EICAR test file and output a message indicating it has found a virus.

---

