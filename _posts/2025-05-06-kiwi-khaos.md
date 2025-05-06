---
title: kiwi Khaos
date: 2025-05-06 15:40:00 +0300
categories: [writeups, ctf, bitsiegectf2025]
tags: [web, lfi, code review]
render_with_liquid: true

---
![kiwi khaos](/assets/img/blogs/kiwi.png)

---

> In this walkthrough, we are going to disect and analyse a wordpress plugin that is vulnerable to a LFI vulnerability.

---

> **Objective** : Perform code review on the given source code, Identify the vulnerability and exploit it to retrieve `flag.txt`.

---

## Kiwi Khaos Walkthrough
1. Navigate to the given URL [Kiwi Khaos](http://54.152.96.1:9100/)
![alt text](/assets/img/blogs/kiwi-khaos/image.png)
2. Observe that it is a WordPress website.
3. Back in the challenge URL, download the attached source code for analysis.
4. After unzipping it, you should get the following files.
![alt text](/assets/img/blogs/kiwi-khaos/image-1.png)
5. Really, people did not understand the challenge: there was only one folder named `kiwiblocks` and the challenge name was `kiwi khaos`..that should have pointed players to investigate that folder.
![alt text](/assets/img/blogs/kiwi-khaos/image-2.png){: .center }
6. Here, I expected players to manually review code or use tools like `Snyk` or even `co-pilot`.
![alt text](/assets/img/blogs/kiwi-khaos/image-3.png)
7. Using Synk, a file inclusion vulnerability is identified in `panel.php` full path `/server-given/challenge-custom/kiwiblocks/src/admin-panel/views/panel.php`
![alt text](/assets/img/blogs/kiwi-khaos/image-4.png)
8. After identifying the path where the vulnerability lies, we can go to the browser and try reading some internal files.
9. Navigating to `http://54.152.96.1:9100/wp-content/plugins/kiwiblocks/src/admin-panel/views/panel.php?tab=../../../../../../../../../../etc/passwd` allows us to read `/etc/passwd` as shown below.
![alt text](/assets/img/blogs/kiwi-khaos/image-5.png)
10. Going back to the source code we can see that the `REDACTED` flag was under the `challenge-custom` folder.
![alt text](/assets/img/blogs/kiwi-khaos/image-6.png)
11. This means if we tried reading `http://54.152.96.1:9100/wp-content/plugins/kiwiblocks/src/admin-panel/views/panel.php?tab=../../../../../../../../../../flag.txt` we would get our flag back.
![alt text](/assets/img/blogs/kiwi-khaos/image-7.png)

---

## Take Aways
Because of time constraints, and an excessive dependence on automated scanners, or a lack of in-depth knowledge of the codebase, I've discovered that many cybersecurity professionals frequently fail to notice subtle but important issues when examining code for vulnerabilities. Although manual review is still crucial, AI-powered assistants like `GitHub Copilot`, which can instantly recommend safer coding patterns, and tools like `Snyk`, which automatically flags known vulnerabilities in dependencies, are becoming more and more useful in closing that gap. Teams can greatly increase their capacity to identify security vulnerabilities early in the development process by fusing human insight with the speed and scalability of these tools.