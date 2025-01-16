# one-liner-chains
Here is presented a chains of tools that are useful for bug-bounty hunting. These chains are helpful for task automation during the reconnaissance phase and vulnerability discovery.

###RECON Chains: 
##Collecting and Resolving subdomains.
'subfinder -d example.com | dnsx -resp-only -silent > resolved_subdomains.txt

''Discovering Live hosts.
"cat resolved_subdomains.txt | httpx -silent -status-code -o live_hosts.txt

*Checking for Subdomain Takeover vulnerability.*
**subfinder -d example.com | dnsx -resp-only | subzy -targets** 

Searching parameters for URL analysis.
gau -o urls.txt example.com && cat urls.txt | qsreplace | tee parameters.txt

XSS scanning using found parameters.
cat parameters.txt | dalfox pipe -o xss_results.txt

SQLi scanning using found parameters.
cat parameters.txt | sqlmap --batch --level=3 --risk=3 --dbs --random-agent

Collecting JavaScript files for analysis.
cat live_hosts.txt | hakrawler -js -plain > js_files.txt

Searching for API keys in js files.
cat js_files.txt | xargs -I % bash -c 'curl -s % | grep -E "(apiKey|secret|token)"'

Dump hidden files from git.
gitdumper http://example.com/.git/ ./dumped_git/

OpenRedirect hunting. 
cat live_hosts.txt | gf redirect | qsreplace 'https://evil.com' | httpx -silent

Collecting e-mails for phishing attacks.
theHarvester -d example.com -b all -f emails.txt

# Bug Bounty Hunting Toolchains

Этот документ представляет собой набор цепочек инструментов, полезных для охоты на баги. Эти цепочки помогают автоматизировать задачи на этапе разведки и обнаружения уязвимостей.

---

## Recon Chains

### 1. **Сбор и разрешение поддоменов**
```bash
subfinder -d example.com | dnsx -resp-only -silent > resolved_subdomains.txt


