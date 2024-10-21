# Access the Command Line
>[!NOTE]
> Access the command line with desktop<br>
> Description: Open a terminal from the desktop environment to interact with Linux


```
Lab Task:
gnome-terminal            # In GNOME desktop
konsole                   # In KDE desktop
xfce4-terminal            # In XFCE desktop
```

>[!NOTE]
> Access the command line with  shell<br>
> Description: Use the  shell to execute commands.
```
Lab Task:
                      # Launch a  shell
echo $SHELL               # Confirm the shell, should show /bin/
```
<br><br>

# Manage Files from the Command Line
>[!NOTE]
> Describe Linux file system <br>
Description: Understand the directory structure of Linux.
```
Lab Task:


ls /                      # List contents of the root directory
ls /etc /var /home         # Explore common system directories
df -h                      # Check mounted file systems and their usage

```

>[!NOTE]
> Manage files with command line<br>
Description: Create, delete, copy, and move files.
```
Lab Task:


touch myfile.txt           # Create an empty file
cp myfile.txt /tmp/        # Copy the file to /tmp directory
mv myfile.txt /home/       # Move the file to your home directory
rm /home/myfile.txt        # Delete the file

```

>[!NOTE]
> Make links between files<br>
Description: Create hard and symbolic links to files.

```
Lab Task:


ln /tmp/myfile.txt hardlink.txt     # Create a hard link
ln -s /tmp/myfile.txt softlink.txt  # Create a symbolic link

```

>[!NOTE]
> Match file names with shell<br>
Description: Use wildcards and shell expansions to match file names.

```
Lab Task:
ls *.txt               # List all files ending with .txt
ls /etc/*config        # List all files in /etc that contain 'config'

```

<br><br>

# Get Help from Linux

>[!NOTE]
> Read manual page<br>
Description: Use man to get help on Linux commands.
```
Lab Task:
man ls                  # View manual page for ls command
man -k disk             # Search for disk-related commands
whatis ls               # Short description of ls command

```
<br><br>

# Create, View, and Edit Files<br>
>[!NOTE]
> Redirect output to a file<br>
Description: Save command output to a file using redirection.

```
Lab Task:
ls /etc > etc_list.txt   # Redirect the output of ls command to a file
cat etc_list.txt         # View the contents of the redirected output

```

>[!NOTE]
> Edit text file from shell<br>
Description: Use text editors like vi or nano to edit files from the shell.

```
Lab Task:
vi myfile.txt            # Open the file in vi editor
nano myfile.txt          # Open the file in nano editor

```

>[!NOTE]
> Change shell environment<br>
Description: Modify shell environment variables and their behavior.

```
Lab Task:
export MYVAR="Hello"     # Set an environment variable
echo $MYVAR              # Display the value of the environment variable
env                      # List all environment variables
unset MYVAR              # Remove an environment variable

```
<br><br>

# Manage Local Users and Groups<br>
>[!NOTE]
> Describe user and group concept<br>
Description: Understand users and groups for managing access and permissions.

```
Lab Task:
id                      # View your user ID, group ID, and groups
groups                   # List groups your user is part of

```

>[!NOTE]
> Gain superuser access<br>
Description: Use sudo to gain superuser access for administrative tasks.

```
Lab Task:
sudo ls /root            # Run a command with superuser privileges
sudo -i                  # Switch to superuser (root) session

```

>[!NOTE]
> Manage local user accounts<br>
Description: Create, delete, and manage users.

```
Lab Task:
sudo useradd newuser     # Create a new user account
sudo passwd newuser      # Set a password for the user
sudo userdel newuser     # Delete the user account

```

>[!NOTE]
> Manage local group accounts<br>
 Description: Create and manage groups for organizing users.

```
Lab Task:
sudo groupadd devgroup   # Create a new group
sudo usermod -aG devgroup newuser   # Add user to a group
sudo groupdel devgroup   # Delete a group
```

>[!NOTE]
> Manage user passwords<br>
Description: Set, update, and manage user passwords.
```
Lab Task:
sudo passwd newuser      # Change the password for a user
sudo chage -l newuser    # View password aging information

```
<br><br>

# Control Access to Files<br>
>[!NOTE]
> Interpret Linux file system permissions<br>
Description: Understand file and directory permissions using the rwx format.

```
Lab Task:
ls -l                    # View file permissions
chmod 755 myfile.txt      # Change permissions of a file

```

>[!NOTE]
> Manage file system permissions<br>
Description: Modify file and directory permissions and ownership.

```
Lab Task:
chown user:group myfile.txt   # Change ownership of a file
chmod u+x myfile.txt          # Add execute permission for the file owner
```

>[!NOTE]
> Manage default permissions<br>
Description: Set default file creation permissions with umask.

```
Lab Task:
umask                       # View current umask
umask 022                   # Set a more permissive umask

```
<br><br>

# Monitor and Manage Processes<br>
>[!NOTE]
> Process start lifecycle<br>
Description: View and manage process lifecycle using ps and other tools.

```
Lab Task:
ps aux                     # View all running processes
top                        # Interactive process monitoring

```

>[!NOTE]
> Control jobs<br>
Description: Manage background and foreground jobs.

```
Lab Task:
sleep 100 &                # Run a job in the background
jobs                       # List background jobs
fg %1                      # Bring a background job to the foreground

```

>[!NOTE]
> Kill processes<br>
Description: Terminate processes using kill.

```
Lab Task:
ps aux | grep sleep         # Find the process ID of a process
kill <PID>                  # Kill the process using its PID
kill -9 <PID>               # Forcefully kill a process

```
>[!NOTE]
> Monitor process activity<br>
Description: Use tools like top and htop to monitor active processes.

```
Lab Task:
top                        # Interactive monitoring of process activity
htop                       # Alternative process monitor (if installed)

```
<br><br>

# Control Service Daemons<br>
>[!NOTE]
> Identify automatically started system processes<br>
Description: List services that start at boot using systemctl.

```
Lab Task:
systemctl list-unit-files --type=service | grep enabled  # List enabled services

```

>[!NOTE]
> Control system services<br>
Description: Start, stop, enable, and disable services.

```
Lab Task:
systemctl start httpd      # Start the Apache service
systemctl stop httpd       # Stop the Apache service
systemctl enable httpd     # Enable Apache to start at boot
systemctl disable httpd    # Disable Apache from starting at boot

```
<br><br>

# Access the remote command line with SSH<br>
>[!NOTE]
Description: Securely access a remote system using ssh.

```
Lab Task:
ssh user@hostname           # Connect to a remote system

```

>[!NOTE]
> Configure SSH-key based authentication<br>
Description: Set up SSH key-based authentication for passwordless login.

```
Lab Task:
ssh-keygen                  # Generate an SSH key pair
ssh-copy-id user@hostname   # Copy your public key to the remote server
ssh user@hostname           # Connect to the remote system without a password
```

>[!NOTE]
> Customize OpenSSH service configuration<br>
Description: Modify SSH server settings.

```
Lab Task:
sudo vi /etc/ssh/sshd_config   # Edit the SSH configuration file
sudo systemctl restart sshd    # Restart the SSH service to apply changes
```
<br><br>

# Analyze and Store Logs

>[!NOTE]
> Describe system log architecture<br>
Description: Understand how system logs are generated and stored.

```
Lab Task:
journalctl -xe              # View detailed log entries
cat /var/log/messages        # View the syslog messages file
```

>[!NOTE]
> Review syslog files<br>
Description: Use cat, tail, and less to examine syslog files.
```
Lab Task:
tail -f /var/log/messages    # Continuously view new log messages
less /var/log/syslog         # View syslog file

```

>[!NOTE]
> Review system journal entries<br>
Description: Use journalctl to query and filter system logs.
```
Lab Task:
journalctl                  # View all journal entries
journalctl --since "1 hour ago"  # Filter logs from the last hour

```

>[!NOTE]
> Preserve the system journal<br>
Description: Configure journald to preserve logs across reboots.

```
Lab Task:
sudo vi /etc/systemd/journald.conf   # Modify the journal configuration
sudo systemctl restart systemd-journald  # Apply the changes


```
>[!NOTE]
> Maintain accurate time<br>
Description: Ensure your system's clock is correct using chrony or ntpd.

```
Lab Task:
timedatectl                     # View current time and time zone
sudo timedatectl set-timezone America/New_York   # Set the system time zone
sudo systemctl restart chronyd   # Restart the NTP service
```
<br><br>

# Manage Networking
>[!NOTE]
> Describe networking concepts<br>
Description: Understand IP addresses, routes, and DNS.

```
Lab Task:
ip addr show                # View the network interfaces and IP addresses
ip route                    # View the routing table

```
>[!NOTE]
> Validate network configuration<br>
Description: Use commands to validate your network setup.

```
Lab Task:
ping google.com             # Test network connectivity
ifconfig eth0               # Display configuration for interface eth0

```

>[!NOTE]
> Configure network from the command line<br>
Description: Use nmcli to configure networking.

```
Lab Task:
nmcli connection show       # View network connections
nmcli device connect eth0   # Connect a device to a network

```
>[!NOTE]
> Edit network configuration files<br>
Description: Manually edit network configuration files.

```
Lab Task:
sudo vi /etc/sysconfig/network-scripts/ifcfg-eth0  # Edit network config

```
>[!NOTE]
> Configure hostnames and name resolutions<br>
Description: Set up the hostname and configure DNS.

```
Lab Task:
hostnamectl set-hostname myserver               # Set the system hostname
sudo vi /etc/hosts                              # Edit the hosts file

```
<br><br>

# Archive and Transfer Files
>[!NOTE]
> Manage compressed tar archives<br>
Description: Compress and extract files using tar.
```

Lab Task:
tar -czvf archive.tar.gz /path/to/directory   # Create a compressed archive
tar -xvzf archive.tar.gz                      # Extract a compressed archive

```
>[!NOTE]
> Transfer files between two systems<br>
Description: Use scp or rsync to transfer files securely.

```
Lab Task:
scp myfile.txt user@remote:/path/to/destination   # Copy file via SCP
rsync -avz mydir user@remote:/path                # Sync directory via rsync

```

>[!NOTE]
> Synchronize files between systems securely<br>
Description: Sync files using rsync over SSH.

```
Lab Task:
rsync -avz /source user@remote:/destination       # Synchronize files securely

```

<br><br>

# Install and Update Software Packages

>[!NOTE]
> Register system for Red Hat support<br>
Description: Use subscription-manager to register for Red Hat support.

```
Lab Task:
sudo subscription-manager register   # Register your system

```

>[!NOTE]
> Explain and investigate RPM software packages<br>
Description: View details about installed RPM packages.

```
Lab Task:
rpm -qa                               # List all installed packages
rpm -qf /bin/ls                       # Identify the package providing a file

```
>[!NOTE]
> Install and update software packages with DNF<br>
Description: Use dnf to manage software packages.

```
Lab Task:
sudo dnf install httpd                # Install Apache web server
sudo dnf update                       # Update all installed packages

```

>[!NOTE]
> Enable DNF repositories<br>
Description: Enable or disable repositories for package management.
```
Lab Task:
sudo dnf config-manager --enable <repo>   # Enable a repository
```

<br><br>

# Access Linux File Systems

>[!NOTE]
> Identify file system and device<br>
Description: View mounted file systems and devices.
```
Lab Task:
df -h                                  # View mounted file systems
lsblk                                  # List block devices
```

>[!NOTE]
> Mount and unmount file systems<br>
Description: Attach and detach file systems.
```
Lab Task:
sudo mount /dev/sdb1 /mnt              # Mount a device to a directory
sudo umount /mnt                       # Unmount a device
```

>[!NOTE]
> Locate files on the system<br>
Description: Use find and locate to search for files.
```
Lab Task:
find / -name "myfile.txt"              # Find a file by name
locate myfile.txt                      # Locate a file using a database
```

<br><br>

# Analyze Server and Get Support

>[!NOTE]
> Analyze and manage remote servers<br>
Description: Remotely access and manage servers using SSH.
```
Lab Task:
ssh user@hostname                      # Connect to a remote server via SSH
```

>[!NOTE]
> Get help from Red Hat customer portal<br>
Description: Access Red Hat support through the customer portal.
```
Lab Task:
Visit Red Hat Customer Portal
```

>[!NOTE]
> Detect and resolve issues with Red Hat <br>
Description: Diagnose and fix system issues with sosreport.
```
Lab Task:
sudo sosreport                        # Generate a diagnostic support report
```


<br><br>


# **Important Linux File Paths and Information**

## **1. `/` - Root Directory**
- **Description**: The top-level directory of the Linux file system. All files and directories stem from this point.

---

## **2. `/bin` - Essential User Binaries**
- **Description**: Contains essential command binaries such as `ls`, `cp`, `mv`, `cat`, `chmod` needed by all users and accessible without mounting other partitions.
  
  - **Example**: 
    - `/bin/ls`: Used for listing directory contents.
    - `/bin/cp`: Used for copying files.

---

## **3. `/boot` - Boot Files**
- **Description**: Contains boot loader files, including the Linux kernel and `initrd` files necessary for booting the system.
  
  - **Example**: 
    - `/boot/grub`: The GRUB bootloader configuration files.
    - `/boot/vmlinuz`: The compressed Linux kernel.

---

## **4. `/etc` - Configuration Files**
- **Description**: Contains system-wide configuration files for all users and services.
  
  - **Example**: 
    - `/etc/fstab`: File system table, defines how disk partitions and file systems are mounted.
    - `/etc/passwd`: Contains user account information.
    - `/etc/hosts`: Static table lookup for hostnames.

---

## **5. `/home` - User Home Directories**
- **Description**: Contains directories for each user account on the system, where personal files and configuration are stored.
  
  - **Example**: 
    - `/home/johndoe`: Home directory for the user `johndoe`.

---

## **6. `/lib` - Essential Shared Libraries**
- **Description**: Contains shared libraries required for system binaries in `/bin` and `/sbin`. Often contains kernel modules as well.
  
  - **Example**: 
    - `/lib/modules`: Kernel modules.
    - `/lib/libc.so.6`: Standard C library, a fundamental part of Linux.

---

## **7. `/opt` - Optional Application Software**
- **Description**: Used for installing additional software packages that are not part of the standard distribution.

  - **Example**:
    - `/opt/google/chrome`: Installation directory for Google Chrome, if installed.

---

## **8. `/proc` - Process and Kernel Information**
- **Description**: A virtual file system containing runtime system information (e.g., system memory, hardware configuration, running processes). It's dynamically created by the kernel.
  
  - **Example**: 
    - `/proc/cpuinfo`: Information about the CPU.
    - `/proc/meminfo`: Information about system memory.

---

## **9. `/root` - Root User’s Home Directory**
- **Description**: The home directory of the `root` (superuser) account.

  - **Example**: 
    - `/root/.bashrc`: Bash configuration file for the `root` user.

---

## **10. `/sbin` - System Binaries**
- **Description**: Contains essential system binaries, typically used by the root user for system administration.

  - **Example**: 
    - `/sbin/reboot`: Command to reboot the system.
    - `/sbin/ifconfig`: Used to configure network interfaces.

---

## **11. `/srv` - Service Data**
- **Description**: Contains data for services provided by the system, such as web servers or file servers.

  - **Example**: 
    - `/srv/www`: Web server data (used by Apache or Nginx).

---

## **12. `/tmp` - Temporary Files**
- **Description**: A temporary directory that applications and the system use for creating temporary files, typically cleared on reboot.

  - **Example**: 
    - `/tmp/log.txt`: Temporary log files.
    - `/tmp/myfile`: Temporary file used by various applications.

---

## **13. `/usr` - User Binaries and Read-only Data**
- **Description**: Contains binaries, libraries, documentation, and source code for second-level programs. It's the largest directory and contains many important subdirectories.

  - **Subdirectories**:
    - `/usr/bin`: User binaries.
    - `/usr/lib`: Libraries for user binaries.
    - `/usr/local`: Locally installed software.
    - `/usr/share`: Shared data such as documentation or icons.

---

## **14. `/var` - Variable Files**
- **Description**: Contains files that are expected to grow in size, such as log files, databases, caches, and other variable data.

  - **Example**: 
    - `/var/log`: System and application log files.
    - `/var/mail`: User mailboxes.
    - `/var/www`: Web server files (for Apache or Nginx).
    - `/var/lib/dpkg`: Files for the package management system (on Debian-based systems).

---

## **15. `/dev` - Device Files**
- **Description**: Contains device nodes representing hardware components (e.g., hard disks, USB devices, terminals).

  - **Example**: 
    - `/dev/sda`: First hard disk.
    - `/dev/tty`: Terminal device.

---

## **16. `/mnt` - Mount Point for Temporary Mounting**
- **Description**: Used to temporarily mount file systems.

  - **Example**: 
    - `/mnt/usb`: A USB drive mounted temporarily.

---

## **17. `/media` - Mount Point for Removable Media**
- **Description**: Used to mount removable media such as CD-ROMs, USB drives, etc.

  - **Example**: 
    - `/media/cdrom`: Mounted CD-ROM.
    - `/media/usb`: Mounted USB drive.

---

## **18. `/sys` - Kernel and Hardware Info (sysfs)**
- **Description**: A virtual file system that provides information about the kernel, devices, and their drivers.

  - **Example**: 
    - `/sys/class/net`: Network device information.
    - `/sys/block/sda`: Information about the block devices.


<br><br>
# **Linux Monitoring and Checking Commands**

## **1. System Level Commands**
- `uptime`
- `top`
- `df -h`
- `free -h`
- `ps aux`
- `systemctl list-units --type=service`
- `journalctl`

## **2. Application Level Commands**
- `systemctl status <service_name>`
- `journalctl -xe`

## **3. Network Level Commands**
- `netstat -tuln`
- `ss -tuln`
- `iftop`

## **4. Hardware Level Commands**
- `lscpu`
- `sensors`
- `sudo lshw`

## **5. OS Level Commands**
- `lsb_release -a`
- `df -i`

## **6. Kernel Level Commands**
- `uname -r`
- `sudo debsums -s`

## **7. Other Commands**
- `iostat`
- `sudo fsck /dev/sda1`
- `du -h --max-depth=1 /`

<br><br>

## **1. Improve Command-line Productivity**

Write Bash Scripts <br>
Description: Create and execute simple bash scripts.
```bash
# Lab Task:
#!/bin/bash
echo "Hello, World!"        # Simple script to display a message
chmod +x myscript.sh        # Make script executable
./myscript.sh               # Execute script
```

> Loop and Condition Constructs in Scripts<br>
Description: Use loops and conditions in bash scripts.
```bash
# Lab Task:
for i in {1..5}; do          # Loop example
  echo "Iteration $i"
done

if [ "$1" -gt 100 ]; then    # Condition example
  echo "Greater than 100"
else
  echo "Less than or equal to 100"
fi
```

> Match Text in Command Line with Regular Expressions<br>
Description: Use regular expressions to match text.
```bash
# Lab Task:
grep "^root" /etc/passwd      # Match lines starting with 'root'
sed 's/[0-9]/X/g' file.txt    # Replace digits with 'X'

```
<br><br>

## 2. Study Future Tasks
> Schedule a Deferred User Job<br>
Description: Use at command to schedule a one-time job.
```bash
# Lab Task:
echo "echo 'Hello'" | at now + 2 minutes   # Schedule a job to run in 2 minutes
atq            # View scheduled jobs
```

> Schedule a Recurring User Job<br>
Description: Use crontab to schedule recurring jobs.
```bash
# Lab Task:
crontab -e                                 # Edit crontab
# Example job to run every day at 2 AM:
0 2 * * * /path/to/script.sh               # Add to crontab
```

> Schedule a Recurring System Job<br>
Description: Use system-wide cron jobs.
```bash
# Lab Task:
sudo vi /etc/crontab                       # Edit system-wide crontab
```
<br><br>

# Add job entry here
> Manage Temporary Files<br>
Description: Manage temporary files in /tmp and /var/tmp.
```bash
# Lab Task:
tmpwatch 24 /tmp                           # Remove files older than 24 hours
```
<br><br>

## 3. Tune System Performance
> Adjust Tuning Profiles<br>
Description: Use tuned-adm to change system performance profiles.
```bash
# Lab Task:
sudo tuned-adm list                        # List available profiles
sudo tuned-adm profile throughput-performance  # Set performance profile
```

> Influence Process Scheduling<br>
Description: Adjust process priority with nice and renice.
```bash
# Lab Task:
nice -n 10 ./myprogram                     # Start a program with lower priority
renice 5 -p 1234                           # Change priority of process with PID 1234
```

<br><br>

## 4. Manage SELinux Security
> Control SELinux File Context<br>
Description: Set and manage SELinux file contexts.
```bash
# Lab Task:
ls -Z                                      # View SELinux context of files
sudo chcon -t httpd_sys_content_t /var/www/html/index.html  # Change file context
```
> Investigate and Resolve SELinux Issues<br>
Description: Troubleshoot SELinux denials.
```bash
# Lab Task:
sudo ausearch -m avc -ts recent            # Search SELinux denials
sudo setenforce 0                          # Temporarily disable SELinux (Permissive mode)
```
<br><br>

## 5. Manage Basic Storage
> Add Partitions, File Systems, and Persistent Mounts<br>
Description: Create partitions and file systems, and configure persistent mounts.
```bash
# Lab Task:
sudo fdisk /dev/sdb                        # Create partition
sudo mkfs.ext4 /dev/sdb1                   # Create file system
sudo blkid /dev/sdb1                       # Get UUID
sudo vi /etc/fstab                         # Add persistent mount entry
```

> Manage Swap Space<br>
Description: Add and manage swap space.
```bash
# Lab Task:
sudo dd if=/dev/zero of=/swapfile bs=1G count=2   # Create a 2GB swap file
sudo mkswap /swapfile                            # Initialize the swap space
sudo swapon /swapfile                            # Enable swap
sudo vi /etc/fstab                               # Add to fstab for persistence
```
<br><br>

## 6. Manage Storage Stack
> Create External Logical Volumes<br>
Description: Use LVM to create and manage logical volumes.
```bash
# Lab Task:
sudo pvcreate /dev/sdb                          # Create physical volume
sudo vgcreate myvg /dev/sdb                     # Create volume group
sudo lvcreate -L 1G -n mylv myvg                # Create a logical volume
sudo mkfs.ext4 /dev/myvg/mylv                   # Create file system
```

> Manage Layered Storage<br>
Description: Manage storage layers with LVM.
```bash
# Lab Task:
sudo lvextend -L +500M /dev/myvg/mylv           # Extend logical volume
sudo resize2fs /dev/myvg/mylv                   # Resize the file system
```
<br><br>

## 7. Access Network-Attached Storage
> Manage Network-Attached Storage with NFS<br>
Description: Mount and configure NFS shares.
```bash
# Lab Task:
sudo mount -t nfs server:/share /mnt           # Mount an NFS share
sudo vi /etc/fstab                             # Add NFS mount to fstab for persistence
```

> Automount Network Storage<br>
Description: Automate mounting of network storage.
```bash
# Lab Task:
sudo vi /etc/auto.master                       # Edit autofs master file
sudo vi /etc/auto.nfs                          # Configure NFS automount points
sudo systemctl restart autofs                  # Restart autofs service
```

<br><br>

## 8. Control the Boot Process
> Select the Boot Target<br>
Description: Change boot target with systemctl.
```bash
# Lab Task:
systemctl get-default                         # Check current boot target
sudo systemctl set-default multi-user.target  # Change to multi-user (non-GUI)
```

> Reset the Root Password<br>
Description: Reset root password in single-user mode.
```bash
# Lab Task:
- Boot into GRUB, edit the boot entry, and append `rd.break` to the kernel line.
- After booting, remount `/sysroot` and reset the password.
```

> Repair File System at Boot<br>
Description: Force file system repair during boot.
```bash
# Lab Task:
sudo touch /forcefsck                         # Force fsck on next boot
```

<br><br>


## 9. Manage Network Security
> Control SELinux Port Labeling<br>
Description: Manage SELinux port contexts.
```bash
# Lab Task:
semanage port -l                              # List current SELinux port labels
sudo semanage port -a -t http_port_t -p tcp 8080  # Add a new port for HTTP
```

> Manage Server Firewall<br>
Description: Use firewalld to manage firewall rules.
```bash
# Lab Task:
sudo firewall-cmd --list-all                  # View current firewall rules
sudo firewall-cmd --add-service=http --permanent  # Add firewall rule for HTTP
sudo firewall-cmd --reload                    # Apply changes
```

<br><br>

## 10. Install Red Hat Enterprise Linux
> Automate Installation with Kickstart<br>
Description: Automate Red Hat installations with kickstart.
```bash
# Lab Task:
sudo vi /root/anaconda-ks.cfg                 # Modify a kickstart file
sudo systemctl start ks.cfg                   # Start kickstart installation
```

> Install and Configure Virtual Machines<br>
Description: Set up virtual machines with virt-manager.
```bash
# Lab Task:
sudo virt-install --name myvm --memory 1024 --vcpus 1 --disk size=10 --cdrom /path/to/iso
```

<br><br>

## 11 Run Containers: Comprehensive Overview
Container Concepts
Description: Containers are lightweight, portable, and consistent environments that encapsulate an application and its dependencies. They isolate applications from the underlying host system, ensuring consistent performance regardless of the host environment.

Lab Task:
```bash

podman run hello-world                        # Run a basic container to verify setup
podman images                                 # List available container images
podman ps -a                                  # List all containers (running or stopped)
podman inspect <container_id>                 # Detailed information about a specific container

```
Deploy a Container
Description: Containers can be used to deploy various applications such as web servers, databases, or custom apps.
Lab Task:
```bash

podman pull httpd                             # Pull an Apache (HTTPD) container image from the registry
podman run -d -p 8080:80 httpd                # Run the Apache container and map port 8080 on host to port 80 in the container
podman ps                                     # List running containers
curl localhost:8080                           # Access the running Apache container via localhost
```

Manage Container Storage and Network Resources
Description: Containers use storage volumes for persistent data and network configurations to communicate with other containers or external systems.
Storage Lab Task:
```bash

podman volume create myvolume                 # Create a persistent volume for containers
podman run -d -v myvolume:/data httpd         # Run a container and attach the volume to /data inside the container
podman volume inspect myvolume                # Inspect the details of the created volume
podman volume ls                              # List all created volumes
podman volume rm myvolume                     # Remove a volume (ensure no container is using it)
```

Network Lab Task:
```bash
podman network create mynetwork               # Create a custom network
podman run -d --network mynetwork httpd       # Run a container attached to the custom network
podman network inspect mynetwork              # Inspect network configuration
podman network rm mynetwork                   # Remove a custom network (ensure no container is using it)
```

Manage Containers as System Services
Description: Containers can be managed like systemd services, allowing them to automatically start at boot, restart on failure, and be controlled like other services on the system.

Lab Task:
Create systemd Service Unit File:
```bash

sudo vi /etc/systemd/system/mycontainer.service
Example of the service file:

ini

[Unit]
Description=MyContainer Service
After=network.target

[Service]
ExecStart=/usr/bin/podman run --rm -d --name mycontainer -p 8080:80 httpd
ExecStop=/usr/bin/podman stop mycontainer
Restart=always

[Install]
WantedBy=multi-user.target

```
Manage the service:
```bash

sudo systemctl daemon-reload                  # Reload systemd to apply changes
sudo systemctl start mycontainer.service      # Start the container service
sudo systemctl enable mycontainer.service     # Enable service to start on boot
sudo systemctl status mycontainer.service     # Check the status of the container service
```

SQL in Containers
Description: Running SQL databases like MySQL, PostgreSQL, or SQLite in containers provides a portable and consistent environment for database management.

SQL Container Lab Task:
```bash

# Pull the MySQL container image
podman pull mysql

# Run MySQL container with an environment variable to set the root password
podman run -d -e MYSQL_ROOT_PASSWORD=mypassword -p 3306:3306 mysql

# Access the MySQL container shell
podman exec -it <container_id> bash

# Run MySQL command line tool inside the container
mysql -u root -p

```
For more advanced database configurations and persistence:
```bash

# Create a persistent volume for MySQL data
podman volume create mysql_data

# Run MySQL container with data volume attached for persistent storage
podman run -d -v mysql_data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=mypassword -p 3306:3306 mysql

```









