# PhishingSecLists
To be used with tools like GoBuster & DirBuster but these lists are specifically tailored and designed for scanning phishing <>< landing pages and other malicious or sketch af websites.

By finding their victim or target lists, you can help prevent further criem. If you can peer behind the curtain of their operation(s), you can dismantle em.

What are they gunna do? Report you to teh cops? lololo

These lists were compiled by looking at the source code of all the popular phishing tool kits out there (blackeye, SET, evilginx2, zphisher, etc) to find what they saved files as, honeypots, and combing through active abuse reports + live phishing landing pages.

![](https://i.giphy.com/media/hQL0xnCrnT3jXn8RJc/giphy.webp)

This is a work in progress █▒▒▒▒▒▒▒▒▒ 10% - Inspired by [SecLists](https://github.com/danielmiessler/SecLists) and many hours of scanning.

protecc ya necc

-------------------
ABOUT TEH LISTS
-------------------

**Wizard.txt** = common filenames and dirs where they might be saving captured credentials, emails, admin and control panel logins, campaign data, etc. A smorgasbord of all targeted industries like finance/crypto/banking/etc.

**Shells.txt** = popular shell file names to scan for

-------------------
EXAMPLE USAGE
-------------------

I like to use gobuster for scanning

![](https://i.imgur.com/BhSrmIb.png)

Scanning a rando phishing page I found on [PhishTank](https://phishtank.com/). It lets us discover there is an l.txt file on root dir that contains user-agent logs. Could be useful to dig through. Could the very first IPs in the logs belong to the attackers while they were setting it up or testing it? Who else has hit this landing page? etc.

Scam lander

![](https://i.imgur.com/g5iDlMS.png)

Discovery of 1.txt

![](https://i.imgur.com/LLzJAOo.png)
