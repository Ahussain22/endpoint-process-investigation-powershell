# 🛡️ Endpoint Investigation Lab – Suspicious PowerShell Activity

## 📌 Objective
To investigate process execution on a Windows 10 machine and identify suspicious behaviour using Event Viewer logs.

---

## 🧠 Scenario
A suspicious PowerShell command was executed on a system. The goal was to analyse logs and determine what actions were performed and whether the behaviour could indicate malicious activity.

---

## 🛠️ Tools Used
- Windows 10 Virtual Machine
- Event Viewer
- PowerShell

---

## 🔧 Step 1: Enable Process Logging

By default, Windows does not log all process activity.

Process creation logging was enabled using Group Policy:
- Enabled **Audit Process Creation**
- Enabled **Include command line in process creation events**

This allows Event ID **4688** to be recorded.

---

## 🔍 Step 2: Generate Activity

Executed the following command:

```
powershell -Command "Start-Process notepad"
```

This simulates PowerShell being used to execute another process.

---

## 🔍 Step 3: Analyse Logs

Navigated to:

Event Viewer → Windows Logs → Security

Filtered logs using:
- **Event ID 4688 (Process Creation)**

---

## 🔍 Step 4: Key Findings

A process creation event showed:

- **NewProcessName:** `C:\Windows\System32\notepad.exe`
- **ParentProcessName:** `powershell.exe`

---

## 🧠 Analysis

The logs show that **PowerShell launched Notepad**, indicating a parent-child process relationship.

This means:
- PowerShell executed a command
- The command created a new process

---

## 🚨 Why This Is Suspicious

- PowerShell is commonly used by attackers for executing commands
- Attackers often use PowerShell to launch other processes
- This behaviour is typical in **fileless malware attacks**

---

## 🛡️ Response Actions

- Investigate PowerShell usage on the system
- Review command execution logs
- Restrict or monitor PowerShell activity
- Run security scans for potential threats

---

## 💡 Key Learning

- Event ID **4688** tracks process creation
- Parent-child relationships reveal how processes are executed
- PowerShell is a high-risk tool often abused in cyber attacks
- Endpoint logs are essential for detecting suspicious behaviour

---

## 📸 Evidence

(Add your screenshot here showing:)
- Event ID 4688
- NewProcessName (notepad.exe)
- ParentProcessName (powershell.exe)

---

## ✅ Outcome

Successfully identified and analysed process execution behaviour, demonstrating how PowerShell can be used to launch other applications and how this can indicate suspicious activity.
