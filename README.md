# blue-team-writeups
A collection of blue team cybersecurity challenge writeups focused on defensive techniques, log analysis, SIEM investigations, and incident response. Includes hands-on labs from platforms like TryHackMe and other SOC-level scenarios.

These writeups are my personal notes and documentation from solving various blue team cybersecurity challenge rooms and simulations. They are intended for educational and reference purposes only.

I do not recommend visiting any external links, domains, or IP addresses that appear in screenshots or text they may be malicious or simulated for training environments only.

These writeups are not intended as professional cybersecurity advice, guidance, or recommendations.

All content is based on my own learning experience from platforms like TryHackMe or other lab environments.

Use this repository at your own discretion and always follow safe cybersecurity practices.

<details>
  <summary><strong>📂 TryHackMe Writeups</strong></summary>

  <br>

  <details>
    <summary><strong>  InvestigatingWindows</strong></summary>

**Q1: What is the version and year of the Windows machine?**  
I first entered `MSInfo` into the Windows search bar to retrieve system information about the machine and determine versions, etc.

**Q2: Which user logged in last?**  
I went into Event Viewer and filtered by event ID `4624` for user logons. I sorted by time to retrieve the last user logon.

**Q3: When did John log onto the system last?**  
I searched for the string `John` in Event Viewer with event ID `4624` and filtered by time again to determine his last login.

**Q4: What IP does the system connect to when it first starts?**  
I restarted the virtual machine. On boot, a PowerShell script pops up briefly. I saw a file path at the top of the PowerShell window:  
`C:\TMP\p.exe`  
From there, I investigated the script to determine what IP it connects to.

**Q5: What two accounts had administrative privileges (other than the Administrator user)?**  
I filtered by event ID `4732`, which logs when a member is added to a security-enabled local group. I found that the `guest` account had been added to the Administrators group, which is quite suspicious.

> 📝 **Note**: `C:\TMP\mim.exe` kept popping up on the virtual machine.

**Q6: What’s the name of the scheduled task that is malicious?**  
I looked for scheduled task creation events (event ID `4698`) in Event Viewer but couldn’t find results.  
So I opened the Task Scheduler via `taskschd.msc`, and browsed the library manually. I identified the malicious task by looking for anything out of the ordinary.

> 🕓 **Task Created**: 3/2/2019 4:56:16 PM

**Bonus – Attacker’s IP (C2 Server)**  
To find the IP address of the attacker’s command and control server, I checked:  
`C:\Windows\System32\drivers\etc\hosts`  
This file contains mappings of IP addresses to hostnames. This confirmed external connections tied to malicious activity.

  </details>

</details>
