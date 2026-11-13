PENETRATION TESTING REPORT
Footprinting and Network Scanning Phases
W2-PM-FINAL  CYBERSECURITY NETWORKWALKS
Pentester Name:Beverley Pedzera
ProgramBatch: B84
Date 2026/11/12
Modules completed: W2-PM2 (GHDB Footprinting Attacks), W2-PM5 (Zenmap Scanning) 
Client/Target: 
1. Public Internet (Search Engines)
 2. My own local LAN Network 
Permission secured?  Yes
Phases covered Phase 
1: Reconnaissance & Footprinting   Phase
 2: Scanning & Network Discovery 

1. Liability Disclaimer
I have performed these activities only on the systems & devices where I had secured written permission or the devices/systems that I own myself. All these materials are for education and research purpose only. Do not use anything from here to break the law. The instructor, the authors and Networkwalks are not responsible for what you do with this knowledge. Every action you take is your own responsibility. Misuse can lead to criminal charges, heavy fines, loss of your job and a permanent record. In most countries unauthorised access is a crime even when nothing is damaged.

2. Introduction
This report covers footprinting the public internet using Google Hacking Database (GHDB) dorks (W2-PM2) and scanning my own local network with Zenmap (W2-PM5). One module covers the footprinting phase and the other covers the scanning phase, so together they show how an attacker moves from gathering public information to mapping live hosts on a network. It is the Week 2 part of my ongoing internship program at Networkwalks.

All searches were performed using web browsers (Google and Shodan), and scanning was done on a Windows PC with Zenmap installed. Every step below includes the exact queries/dorks used, the result I observed, and a short note on why the finding matters from an attacker's point of view.

3. Tools Used
•	Google / Exploit-DB GHDB  - Source for Google dorks to find exposed devices and files. 
•	Shodan.io  - Search engine used to find raw IP addresses of exposed cameras. 
•	Zenmap (Nmap GUI) - Scan the local subnet to find live hosts, IPs, and MAC addresses. 
•	Windows CMD -Local IP and MAC address identification (`ipconfig`). 

4. Activities Performed
4.1 Footprinting & Reconnaissance (W2-PM2)
I performed reconnaissance against the public internet to find devices and files that owners unintentionally exposed. I used the Exploit-DB GHDB to source search queries (dorks).
For Task 1, I used camera-related dorks such as `intitle:"webcamXP 5"` and `intitle:"Live View / - AXIS"`. Because Google often returns dead links or blog posts, I also used  Shodan.io  and searched for `webcamXP` to find raw IP addresses of live, unsecured security cameras. 
For Task 2, I used dorks like `intitle:"index of" mathematics pdf` and `intitle:index.of "parent directory" mathematics pdf` to find misconfigured web servers. These servers were publicly listing and exposing downloadable mathematics e-books in PDF format without requiring any authentication. I successfully recorded 10 camera links and 10 open directories for the final report.

 Task 1: Live Security Cameras
| No. | Link | Relevant Dork | Username /Password |
| :--- | :--- | :--- | :--- |
| 1 | `https://www.lmc.edu/webcam.htm` | `intitle:"Webcam" inurl:WebCam.htm` | None |
| 2 | `http://75.149.26.30` | `intitle:"webcamXP 5"` | Login Prompt |
| 3 | `http://195.165.139.229` | `intitle:"Live View / - AXIS"` | None |
| 4 | `http://110.54.192.11` | `intitle:"Toshiba Network Camera"` | Login Prompt |
| 5 | `http://84.12.98.1:8080` | `intitle:"webcamXP" inurl:8080` | None |
| 6 | `http://173.23.18.110` | `intitle:"Microseven M7CAM IP Camera"` | None |
| 7 | `http://209.141.55.26` | `intitle:"Device(IP CAMERA)" "language" -comInet` | None |
| 8 | `http://67.205.12.15` | `intitle:"Network Camera" inurl:main.cgi` | Login Prompt |
| 9 | `http://192.99.14.13` | `intitle:"IP camera login page"` | None |
| 10 | `http://45.33.12.1` | `intitle:"Login" intitle:"camera"` | Login Prompt |

Task 2: Mathematics PDFs
| No. | Link | Relevant Dork | Username /Password |
| :--- | :--- | :--- | :--- |
| 1 | `https://www.skylineuniversity.ac.ae/pdf/math/` | `intitle:index.of "parent directory" mathematics pdf` | None |
| 2 | `https://www.maths.ed.ac.uk/~v1ranick/papers/` | `intitle:"index of" mathematics pdf` | None |
| 3 | `https://www.math.ucla.edu/~tao/preprints/` | `intitle:"index of" mathematics` | None |
| 4 | `http://www.math.uni-bielefeld.de/~sillke/` | `intitle:"index of" /math/ pdf` | None |
| 5 | `https://www.math.stonybrook.edu/~bishop/` | `intitle:"index of" "linear algebra" pdf` | None |
| 6 | `http://www.maths.manchester.ac.uk/~gm/` | `intitle:"index of" calculus pdf` | None |
| 7 | `http://www.math.uni-bonn.de/people/` | `intitle:"index of" algebra pdf` | None |
| 8 | `http://www.math.toronto.edu/mathnet/` | `intitle:index.of "parent directory" math` | None |
| 9 | `http://www.math.utah.edu/~treiberg/Math.html` | `intitle:"index of" math` | None |
| 10 | `http://www.math.uni-hamburg.de/home/` | `intitle:"index of" "parent directory"` | None |

4.2 Network Scanning with Zenmap (W2-PM5)
For the second activity, I used Zenmap to perform network discovery on my local network. I first used the Windows `ipconfig` command to identify my local IP address (192.168.1.3) and LAN subnet (192.168.1.0/24). 
I then entered the subnet into Zenmap and selected the "Ping scan" profile to identify active hosts. The scan successfully identified  6 live hosts on my network. I recorded the IP addresses (192.168.1.1, 192.168.1.2, 192.168.1.3, 192.168.1.5, 192.168.1.24, 192.168.1.25) and their corresponding MAC addresses.

After completing the scan, I opened the Topology section in Zenmap, enabled the legend, and saved the network topology in PDF format as required by the practical task.

 5. Risk Analysis / Impact
Based on the information collected during the footprinting and network scanning activities, I identified the following potential risks.

| # | Risk / Finding | Evidence / Observation | Potential Impact | Risk Level |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Exposed Live Camera | GHDB and Shodan returned active camera login pages | Unauthorized users could view live feeds, violating privacy. | **Critical** |
| 2 | Exposed Open Directories | Found servers listing math PDFs without authentication | Data leakage; attackers can download proprietary or copyrighted files. | **Medium** |
| 3 | Multiple live hosts visible | Zenmap identified 6 live hosts on my local network | Unknown or unauthorized devices may potentially be present on a network. | **Medium** |
| 4 | MAC Addresses exposed | Ping scan revealed MAC addresses of local devices | Attackers could use MAC addresses to bypass MAC filtering or spoof devices. | **Low** |

Risk level key: Critical, Medium, Low. The risks above are observations from the exercises, not confirmed exploitable vulnerabilities.

6. Recommendations
Based on the observations from these activities, I recommend the following security improvements:
•	Secure Exposed Devices: Change default passwords on cameras and place them behind a firewall. Never expose them directly to the internet.
•	Configure Web Servers Correctly: Disable directory listing (indexing) on web servers to prevent open directories from exposing files.
•	Regular Network Discovery: Organizations should periodically scan their own networks to identify active devices and investigate any unknown devices.
•	Maintain Network Documentation: Network topology and device information (IPs and MACs) should be documented and updated regularly.

7. Conclusion
During Week 2 of my Cybersecurity & Ethical Hacking internship, I completed practical activities covering footprinting, reconnaissance, and network scanning.
In the footprinting activity, I learned how Google dorks can be used to find sensitive data and exposed devices. I also learned the importance of using alternative tools like Shodan when standard search engines are insufficient.
In the network scanning activity, I used Zenmap to identify my local network configuration and discover active hosts, IPs, and MAC addresses. I also created and saved a network topology map.
The exercises showed me that information gathering is an important part of cybersecurity. Even before attempting to exploit a system, a security professional can learn a significant amount about an environment by carefully analyzing publicly available information and network responses.

8. Evidences Collected
Screenshots collected as evidence during the activities:s
 
<img width="940" height="309" alt="image" src="https://github.com/user-attachments/assets/6c042dab-52ba-42ae-ab0f-8ecc917b5731" />
<img width="940" height="446" alt="image" src="https://github.com/user-attachments/assets/d9577595-bd50-44c6-9ed5-47f8119cdb7e" />


 







