# Restoring User Access to a Network Home Folder (macOS)

### Summary

This case demonstrates structured troubleshooting of user access issues, clear communication with non-technical users, and validation-based resolution of production IT systems.

### Context

* **Environment:** Campus IT at Pomona College
* **Users:** Faculty and students
* **Systems:** macOS endpoints, network-based home folders accessed via WebDAV
* **Impact:** User unable to access personal network storage required for academic or administrative work


### Problem Statement

A user reported they were unable to access their network home folder on their Mac, preventing them from opening and saving required files. The issue occurred both on and off campus, and the user was unsure whether the problem was related to their account or their device.


### Clarifying Questions

To scope the issue, I asked:

* Which operating system and device are you using?
* Have you accessed this folder successfully before?
* Are you currently on campus or off campus?
* Are you seeing an error message, or does the connection fail silently?
* Have there been any recent changes such as a password reset or OS update?

This helped determine the issue was **device-specific**, not a system-wide outage.



### Reproduction Steps

1. Opened **Finder** on macOS
2. Selected **Go → Connect to Server** (Command + K)
3. Entered the WebDAV server address:
   `https://webdav.pomona.edu`
4. Authenticated using the user’s campus credentials
5. Attempted to access the user-specific directory (e.g., `jlr12011`)

The connection failed to expose the user’s folder.



### Diagnostics

To isolate the root cause, I:

* Verified the user’s credentials by confirming access to other campus services
* Confirmed the correct server address and protocol were being used
* Compared the setup against a known-good configuration
* Checked whether the issue followed the user or remained isolated to the device
* Verified network connectivity and off-campus access requirements

These checks ruled out account issues and pointed toward a **local configuration problem**.



### Root Cause

The issue was caused by an incorrect or incomplete WebDAV connection setup, preventing proper authentication and access to the user’s designated network directory.



### Resolution

* Guided the user through reconnecting to the server using the correct WebDAV configuration
* Ensured authentication completed successfully
* Navigated to the correct user-specific folder
* Confirmed read and write access to files



### Validation

* User successfully opened existing files
* User created and saved a new file to the folder
* Folder remained accessible after disconnecting and reconnecting



### Prevention & Documentation

* Explained correct connection steps for future use
* Documented the resolution for reuse on similar tickets
* Flagged the issue as a common configuration-related failure

