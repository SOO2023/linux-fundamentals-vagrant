# Linux Fundamentals with Vagrant

---

### **Set Up a Vagrant Server**

**Screenshot #1: Vagrant initialization and SSH login**
![Vagrant init1](https://github.com/user-attachments/assets/db30df0e-fc24-40aa-95bf-e3382f7d3c61)
![Vagrant init2](https://github.com/user-attachments/assets/14146645-8719-4f18-bec3-8eb13b55fe6d)

**Description:**
I initialized a new Vagrant environment using the `generic/alpine318` box with `vagrant init generic/alpine318`. To optimize performance on my low-memory PC, I updated the `Vagrantfile` to allocate only 1 CPU and 128MB of RAM. After running `vagrant up`, I successfully booted the virtual machine and accessed it via SSH. The prompt confirms I am inside the VM at the `/home/vagrant` directory.

---


### **Explore the Linux File System**

**Screenshot #2: Custom folder structure created**
![image](https://github.com/user-attachments/assets/16e3eed5-f8e2-46ed-a950-e1e1683fa163)

**Description:**
Inside the VM home directory (`/home/vagrant`), I created a custom folder structure using `mkdir`. The structure includes a `projects` directory, which contains a subdirectory named `devops`. This helps organize development work and separates different project types or environments under clearly labeled folders.

---


### **Manage File Permissions and Ownership**

**Screenshot #3: File permission change**
![image](https://github.com/user-attachments/assets/e604c447-4a82-4e9f-8bf2-eb107c59a06f)

**Description:**
I created a file named `hello.txt` and initially confirmed that the file was owned by the user `vagrant` with default permissions (`-rw-r--r--`).
* I then used `chmod 000 hello.txt` to remove all permissions, which resulted in a "Permission denied" error when trying to read or execute the file.
* Using `chmod 700 hello.txt`, I restored full permissions for the owner (`rwx------`), allowing me to read the file again.

**Screenshot #4: File ownership change**
![image](https://github.com/user-attachments/assets/85034d63-e4c1-4379-b672-61182eabbcb6)

**Description:**
Still using the last modified state of the `hello.txt` file.
* I changed the ownership to `root` using `sudo chown root:root hello.txt`, which made it inaccessible to `vagrant`.
* Finally, I changed the **group ownership** back to `vagrant` using `sudo chown :vagrant hello.txt`, and then updated the file’s permissions to `740` using `chmod 740 hello.txt`. This means:
  * The **owner** (`root`) has full permissions: **read (r), write (w), and execute (x)**.
  * The **group** (`vagrant`) has **read-only (r)** access.
  * **Others** have **no permissions** at all (`---`).

This exercise demonstrates how `chmod` and `chown` control file access by adjusting permissions and ownership at the user and group levels.

---

### **Install and Configure a Package**

**Screenshot #5: Package installation and version check**

![image](https://github.com/user-attachments/assets/15a7c022-9062-4f5d-b1db-4a874552f000)

**Description:**
I installed the `curl` utility using Alpine’s package manager with the command `sudo apk add curl`. After the installation, I verified the installed version using `curl --version`, which confirmed that version **8.5.0** was successfully installed.

---


### **6. Test Remote Connectivity**

**Screenshot #6: Ping result**
![ping](https://github.com/user-attachments/assets/46e8f8c4-af72-479c-bbff-6e6711640d34)

**Description:**
I used the `ping` command with `-c 4` to send four ICMP echo requests to `google.com`. The result shows successful communication with 0% packet loss and a round-trip average time of approximately **52 ms**.

This confirms that the virtual machine has active internet access, and the network connection is functioning properly — a crucial step before performing updates, downloading packages, or configuring remote tools.
