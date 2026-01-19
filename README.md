# Splunk Lab Deployment
Deployment & System Remediation Lab 
Splunk Enterprise: Deployment & System Remediation Lab
Date: January 19, 2026
Role: Security Analyst 
Systems Administrator (Lab)

## Overview
Successfully deployed Splunk Enterprise 10.2.0 on Windows 11 following a critical MSI database corruption (Error 1610).

## Technical Challenges & Resolutions
* Persistent Identity Resolution: Encountered a "Service Already Exist" deadlock during re-installatiin attempts. This took the most time!
* Manual Stage Purging: Discovered that Splunk stores unique indentifiers in instance.cfg and identity.data that survive standard uninstalls.
* Artifact Cleanup: Performed iterative manual purges of the etc/auth and var/lib/splunk directories to ensure the new installation could generate a fresh system identity.
* Registry Remediation: Utilized PowerShell to purge orphaned product GUIDs from the `S-1-5-18` UserData hive after standard uninstallers failed.
* Service Deadlock Recovery: Resolved an SCM "Waiting to start" hang by force-terminating zombied `splunkd` processes and clearing `.pid` lock files.
* Credential Injection: Manually initialized the administrative security principal via `user-seed.conf` to bypass Web UI initialization failures.
* 

## Operational Milestones
* Verified data ingestion for Windows System & Security event logs.
* Developed custom search queries for hardware state monitoring (Kernel-Power).
* Constructed a real-time health dashboard utilizing statistical pivoting.

* In very basic terms I attempted to uninstall/then re-install (license ran out!) "Splunk" but it said a file already existed. Even after I "Deleted" in "Local Disk (C:). There was still a "hold up" somewhere and I had to find exactly where.
* This led to 4+ hours of deep diving and introducing me to "Powershell" & finding out what the "Registry" was and what it contained. Once I purged the system the installer became issue and I had to reconfig.
* There was a lot more involved but I learned that just because you "delete" a file, it can still linger in the background and cause a mess when you want to re-install, by "holding on" and won't leave without a fight.
* Next on my list is to get more familiar w/ Splunk!

