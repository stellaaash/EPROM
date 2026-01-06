---
tags:
  - Windows
---
The NTFS is the file system primarily used on modern Windows systems.
It provides journaling, which allows for restoration of damage to the file system when needed.
# Permissions
On Windows, visible under `Properties -> Security`.
- **Read**
- **Write**
- **Read & Execute**
- **List Folder Contents**
- **Modify**
- **Full Control**
# Alternate Data Streams
NTFS allows files to **have multiple data streams beside the main file content**.
This allows metadata or even hidden files adding information to be attached to a file without modifying its actual contents.
Problem is, this feature is often used by malware to hide malicious code or other bad content.
This is problem because the file explorer of Windows doesn't show alternate data streams.
**You can access data streams by using a semi-colon after the file name: `echo "wow" > file.txt:mystream`.**