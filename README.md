First, the server's IP address was added to the /etc/hosts file, allowing access via its domain name. Then, an nmap scan was performed, revealing two open ports: 80 (HTTP) and 22 (SSH).

A directory enumeration was conducted using GoBuster, leading to the discovery of the /assets directory. Further examination of this directory revealed potential command injection in index.php via the cmd parameter. This allowed listing files on the server, including index.php, images, and styles.css.

Next, the /etc/passwd file was accessed, with its contents encoded in Base64. After decoding, a user named Deku was identified.

A Reverse Shell connection was established using netcat, granting access to the system as www-data.

Further exploration revealed various files, including oneforall.jpg, which was transferred to the attacking machine. Analysis of the file’s headers showed an incorrect format, which was fixed using hexedit. Afterward, steganography (steghide) was used to extract a hidden text file, creds.txt, containing credentials for the Deku user.

After logging in via SSH with Deku’s credentials, a privilege escalation check (sudo -l) was performed. It was discovered that Deku had permission to edit the feedback.sh script, which was executed with root privileges. By modifying this script, Deku was added to the sudoers file with NOPASSWD:ALL rights, granting full control over the system (root access).

Thus, the school.thm server was successfully compromised.
