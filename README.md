# PhishingSecLists
To be used with scanning tools like [GoBuster](https://github.com/OJ/gobuster), [ffuf](https://github.com/ffuf/ffuf), Burp Suite, and DirBuster but these lists are specifically tailored and designed for scanning phishing <>< landing pages and other malicious or sketch af websites.

By finding their victim or target lists, you can help prevent further harm. If you can peer behind the curtain of their operation(s), you can dismantle em. Finding these files will give you a lot of valuable intel to pivot from or act on.

The websites of Threat Actors make perfect targets to scan and cut your teeth on. What are they gunna do? Report you to teh cops? lol

These lists were compiled by looking at the source code of all the popular phishing tool kits out there (blackeye, SET, evilginx2, zphisher, etc) to find what they saved files as, honeypots, and combing through active abuse reports + live phishing landing pages.

Languages represented in the list: English, Spanish, Hindi, Russian, Chinese, Malay, Thai, Tamil, Khmer, Indonesian, and Swahili.

To note: this method has a low success rate. Out of scanning 100 unique phishing/malicious websites, you may only get 4-5 hits BUT the intel you find when you do get a good valid hit is extremely valuable. 

When using ffuf, you can dump all your phishing urls into a domains.txt and scan many websites at once to increase your hit percentages.

ex: ffuf -w domains.txt:DOMAIN -w Wizard.txt -u DOMAIN/FUZZ -c -mc 200 -t 75

![](https://i.giphy.com/media/hQL0xnCrnT3jXn8RJc/giphy.webp)

This is a work in progress ██▒▒▒▒▒▒▒▒ 23% - Inspired by [SecLists](https://github.com/danielmiessler/SecLists) and many hours of scanning.

protecc ya necc

-------------------
ABOUT TEH LISTS
-------------------

**Wizard.txt** = common filenames and dirs where they might be saving captured credentials, emails, admin and control panel logins, campaign data, etc. A smorgasbord of all targeted industries like finance/crypto/banking/etc.

**Shells.txt** = popular shell file names to scan for

-------------------
EXAMPLE USAGE
-------------------

I like to use [gobuster](https://github.com/OJ/gobuster) for scanning. [ffuf](https://github.com/ffuf/ffuf) is also really nice.

Example 1:

![](https://i.imgur.com/BIYi1dr.png)

Scanning a rando phishing page I found on the [Crypto Phishing Threat Intel Feed](https://github.com/spmedia/Crypto-Scam-and-Crypto-Phishing-Threat-Intel-Feed). It lets us discover there is an `l.txt` file on root dir that contains user-agent logs. Could be useful to dig through. Could the very first IPs in the logs belong to the attackers while they were setting it up or testing it? Who else has hit this landing page? etc. It also lets us know there is a /controlpanel (commonly cPanel) and /webmail on the box.

Scam landing page

![](https://i.imgur.com/g5iDlMS.png)

Discovery of `l.txt` that has user-agent and IP logs in it

![](https://i.imgur.com/LLzJAOo.png)

Example 2:

Discovery of an open `/scripts/` dir on a scam landing page with some interesting files in it

![](https://i.imgur.com/FDZ7fXI.png)

Example 3:

A scan of an "American financial firm" scam website reveals an `admin/login` page which has Chinese chars and has `<html lang="zh">` in the source. The language code zh is the ISO 639-1 standard code for the Chinese language. This lets us know the threat actors behind this scam might be Chinese.

![](https://i.imgur.com/Z2XmRbm.png)

Example 4:

A scan of a Ledger crypto scam website reveals an `a.txt` which has a list of IPs. Is this a blocklist? Is it a log of victims who have hit this site? Good thing to investigate.

![](https://i.imgur.com/tIEomaU.png)

Discovery of this type of info is awesome! This gives you new enhanced addtional intel to go off of for your investigation and OSINT gathering. Some people really be leaving the wildest and easiest files to discover on their scam and malicious landers.

Greetz to all the CTI and data nerds out there and the DEFCON225 homies who help w scanning!
