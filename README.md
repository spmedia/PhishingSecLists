# PhishingSecLists
This script is to be used with web scanning tools ([Gobuster](https://github.com/OJ/gobuster), [ffuf](https://github.com/ffuf/ffuf), Burp Suite, DirBuster). These lists are specifically tailored and designed for fuzzing phishing, crypto scam landing pages, and other malicious sketch af websites. 

By finding their victim or target lists, you can help prevent further harm. If you can peer behind the curtain of their operation(s), you can dismantle em. Finding these files will give you a lot of valuable intel to pivot from or act on.

The websites of Threat Actors make perfect targets to scan and cut your teeth on. What are they gunna do? Report you to teh cops? lol

These lists were compiled by looking at the source code of all the popular phishing tool kits out there (blackeye, SET, evilginx2, zphisher, etc) to find what they saved files as, honeypots,  combing through active abuse reports, sitting in skid fraudster chats, and live phishing landing pages.

Languages represented in the list: Burmese, Cambodian, Chinese, English, Hindi, Indonesian, Khmer, Nigerian Pidgin, Malay, Russian, Spanish, Swahili, Tamil, Thai, and Ukrainian.

To note: this method has a low success rate. Out of scanning 100 unique phishing/malicious websites, you may only get 4-5 hits BUT the intel you find when you do get a good valid hit is extremely valuable.

You can also use this list to find hits when scanning Tor hidden service .onion domains as well. 

![](https://i.imgur.com/eiMP4bb.png)

This is a work in progress █████▒▒▒▒▒ 54% - Inspired by [SecLists](https://github.com/danielmiessler/SecLists) and many hours of scanning.

protecc ya necc


# ABOUT TEH LISTS ℹ️

**Wizard.txt** = beware traveller, this sacred scroll holds dominion over the darkest crypto enchantments. common filenames and dirs where they might be saving captured credentials, emails, admin and control panel logins, campaign data, etc. A smorgasbord of all targeted industries like finance/crypto/banking/etc.

**Shells.txt** = popular shell file names to scan for


# EXAMPLE USAGE 👀

I like to use [gobuster](https://github.com/OJ/gobuster) for scanning. [ffuf](https://github.com/ffuf/ffuf) is also really nice.

Example 1:

![](https://i.imgur.com/BIYi1dr.png)

Scanning a rando phishing page I found on the [Crypto Phishing Threat Intel Feed](https://github.com/spmedia/Crypto-Scam-and-Crypto-Phishing-Threat-Intel-Feed). It lets us discover there is a `l.txt` file on root dir that contains user-agent logs. Could be useful to dig through. Could the very first IPs in the logs belong to the attackers while they were setting it up or testing it? Who else has hit this landing page? etc. It also lets us know there is a /controlpanel (commonly cPanel) and /webmail on the box.

Scam landing page

![](https://i.imgur.com/g5iDlMS.png)

Discovery of `l.txt` that has user-agent and IP logs in it

![](https://i.imgur.com/LLzJAOo.png)

Example 2:

Discovery of an open `/scripts/` dir on a scam landing page with some interesting files in it.

![](https://i.imgur.com/FDZ7fXI.png)

Example 3:

A scan of an "American financial firm" scam website reveals an `admin/login` page which has Chinese chars and has `<html lang="zh">` in the source. The language code zh is the ISO 639-1 standard code for the Chinese language. This lets us know the threat actors behind this scam might be Chinese.

![](https://i.imgur.com/Z2XmRbm.png)

Example 4:

A scan of a Ledger crypto scam website reveals an `a.txt` which has a list of IPs. Is this a blocklist? Is it a log of victims who have hit this site? Good thing to investigate.

![](https://i.imgur.com/tIEomaU.png)

Discovery of this type of info is awesome! This gives you new enhanced addtional intel to go off of for your investigation and OSINT gathering. Some people really be leaving the wildest and easiest files to discover on their scam and malicious landers.

Example 5:

While scanning a crypto exchange scam website, the discovery of a `/interface` page which leads us to a `/top` section. It's some internal invite stats system that shows how many invites have been sent out and how much each invite/user has generated the scammers. No login required to view this. The gmails look like potential victims who are wrapped up in this scam or it could even be the scammers personals emails... good data to investigate off of.

![](https://i.imgur.com/maI0O5B.png)

Example 6:

Scanning a ransomware groups .onion URL let me find a `/server-status` page that reveals some interesting information...

![](https://i.imgur.com/n08q9ox.png)

Example 7:

Fuzzing a crypto exchange scam URL lets us find a `index.zip` that they failed to delete after setup which lets us download the entire phishing landing page. Digging thru the source lets us understand how this scam is setup. Are there hardcoded API keys or wallet addresses? How is the entire thing setup? etc.

![](https://i.imgur.com/QSTm3z0.png)

Example 8:

The discovery of a `/admin/index.html` and `/admin/login.html` on a crypto scam website that's using a popular Chinese panel called KIT ADMIN. Hitting the index.html lets us temporarily see the backend admin panel of this scam site before redirecting us to `login.html`. If you stop the redirect using burp, it gives you full unauth'd access to its backend admin panel of the entire scam site 👀😍

![](https://i.imgur.com/U8k3e2r.png)

lol RIP - you now have full access to the scam site and can do whatever you want - we also learn and can see that the admin's name is set to `Van`. Van is a common name in Vietnam.

![](https://i.imgur.com/5CJjQZY.png)

Example 9:

A curious hit for `in.txt` on a fake crypto exchange phishing site. when we visit it, we see a note left by a hacker who was here before us. kinda awesome! its like a relic from a historical hacker past.

![](https://i.imgur.com/ooIcOe7.png)


Example 10:

A hit for `data.zip` on a crypto scam website in the root dir. DLing it lets us access the source code for the entire website and see how they have it setup and it contains hardcoded creds, crypto wallet addresses, and api keys. The `.DS_Store` hit is also interesting, it lets us know the opps behind the site are macOS users. 

![](https://i.imgur.com/YEOiGb7.png)

From the source code, its seemingly some China scammer bros.

(translated == Authorized address)
```
//授权地址 
let address = 'TFRsDKmRBqJXEJFFcq8Gzmoo9otg6aUre8'
```

&

(translated == Get address)
```
async function ethBalance() {
    getWeb3().then(async res => {
        window.web3 = res;
        let contractAddress = "0xdAC17F958D2ee523a2206206994597C13D831ec7";
        window.contract = new window.web3.eth.Contract(
            ABI,
            contractAddress
        );
        // todo 获取地址
```


# Commands / Quick Cheat Sheet 📃

This is just a quick lil reference section to help you increase your odds of finding a hit and getting around certain blocks.

When using ffuf, you can dump all your phishing urls into a domains.txt and scan many websites at once to increase your hit percentages.

and then do:
##
    ffuf -w domains.txt:DOMAIN -w Wizard.txt -u DOMAIN/FUZZ -c -mc 200 -t 75

to change the ffuf user-agent (default one is straight up `Fuzz Faster U Fool` which is commonly blocked by some systems):
##
    ffuf -w Wizard.txt -u https://example.com/FUZZ -c -t 75 -mc 200 -H "User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36"             

to scan targets using Tor exit proxies + change user-agent (make sure you do `service tor start` first before scanning):
##
    ffuf -w Wizard.txt -u https://example.com/FUZZ -c -t 75 -mc 200 -H "User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36" -x socks5://127.0.0.1:9050


to scan .onion hidden service URLs + change user-agent (make sure you do `service tor start` first before scanning):
##
    ffuf -w Wizard.txt -u http://oow7rehrxlzpy6vh3hezl2khstkpa6s7wx3iit74tr6xbjibupld5iad.onion/FUZZ -c -t 75 -mc 200 -H "User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36" -x socks5://127.0.0.1:9050
    

# Greetz 🙏


All the CTI and data nerds who are in the trenches and fuzzing stuffs, tk0, joohoi, rj2, SP, all the powerful wizards out there, <a href="https://cybersecuritystickers.com/">Cybersecurity Stickers</a> and the DC225 homies who help w scanning!


# Star History ⭐

<a href="https://star-history.com/#spmedia/PhishingSecLists&Date">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos=spmedia/PhishingSecLists&type=Date&theme=dark" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/svg?repos=spmedia/PhishingSecLists&type=Date" />
   <img alt="Star History Chart" src="https://api.star-history.com/svg?repos=spmedia/PhishingSecLists&type=Date" />
 </picture>
</a>
