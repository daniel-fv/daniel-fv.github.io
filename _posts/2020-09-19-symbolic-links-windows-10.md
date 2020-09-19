---
title: "Using symbolic links in Windows 10"
date: 2020-09-19
tags: [Windows 10, posts]
---
Posting this to remind me in the future.

I always like to keep my GitHub files syncronized with OneDrive but I also don't like the long folder structure. I try to keep it short while keeping the benefits of storing my files in OneDrive by using **symbolic links**.

In this example I want to easily change the directory to *C:\Github* while actually browsing my OneDrive folder.

```powershell
 mklink /D C:\Github 'C:\Users\myname\OneDrive\Documents\GitHub\'
```

Where:

**/D** - create symbolic link to directory option

**C:\GitHub** - symbolic link

**C:\Users\myname\OneDrive\Documents\GitHub** - symbolic link destination

---
Reference:

- <https://www.techrepublic.com/blog/windows-and-office/be-more-efficient-and-better-organized-with-the-mklink-symbolic-link-tool/>