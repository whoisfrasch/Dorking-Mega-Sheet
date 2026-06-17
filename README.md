# Dorking Mega-Sheet 
> Replace `example.com` / `Example Corp` everywhere with your target.

---

## 0. Cross-Engine Operator Matrix

| Goal | Google | Bing | Yandex | DuckDuckGo | Brave |
|---|---|---|---|---|---|
| Domain | site: | site: | site: / host: / rhost: | site: | site: |
| URL part | inurl: | inurl: | inurl: / url: | inurl: | inurl: |
| Title | intitle: | intitle: | title: | intitle: | intitle: |
| Body | intext: | inbody: | intext: | intext: | intext: |
| Filetype | filetype: / ext: | filetype: / ext: | mime: / filetype: | filetype: | filetype: |
| Anchor text | inanchor: | inanchor: | anchor: / anchorint: | — | — |
| Exact | "..." | "..." | "..." | "..." | "..." |
| OR | OR / \| | OR | \| | OR | OR |
| Proximity | AROUND(n) | near:n | && / /n | — | — |
| Exclude | - | - | - / ~~ | - | - |
| Wildcard | * | — | * | — | — |
| Date | before: after: | — | date: | — | — |
| Region | cr=countryDE in URL | loc:DE | — | region:de-de | — |
| Feed | — | feed: / hasfeed: | — | — | — |
| IP / range | — | ip: | ip: | — | — |

Google has effectively killed `cache:`, `+`, and `link:`, and `AROUND` is unreliable. For a lot of what follows, Yandex is strongest (real wildcards, host:, mime:) and Bing has unique ip:/feed:/inbody:. Always run the same dork across several engines.

---

## PART A — TECHNICAL (Browser-Only)

### A1. Config / Secret Files

```text
site:example.com ext:env
site:example.com ext:env intext:DB_PASSWORD
site:example.com ext:env intext:SECRET
site:example.com ext:env intext:APP_KEY
site:example.com ext:env intext:STRIPE
site:example.com filetype:env "MAIL_PASSWORD"
site:example.com ext:cfg OR ext:conf OR ext:config
site:example.com ext:ini intext:password
site:example.com ext:yml OR ext:yaml intext:password
site:example.com ext:yaml intext:"private_key"
site:example.com ext:properties intext:jdbc
site:example.com ext:toml intext:token
site:example.com ext:json intext:"api_key"
site:example.com ext:json intext:"client_secret"
site:example.com ext:json intext:"aws_secret_access_key"
site:example.com filetype:xml intext:"connectionString"
site:example.com filetype:reg intext:password
site:example.com ext:sh intext:"export AWS_"
site:example.com ext:ps1 intext:ConvertTo-SecureString
site:example.com inurl:Dockerfile intext:ENV
site:example.com inurl:docker-compose ext:yml intext:password
site:example.com inurl:".npmrc" intext:_authToken
site:example.com inurl:".dockercfg" OR inurl:".docker/config.json"
site:example.com inurl:"web.config" intext:password
site:example.com inurl:"settings.py" intext:SECRET_KEY
site:example.com inurl:"local.settings.json"
site:example.com inurl:"application.properties"
site:example.com inurl:"appsettings.json" intext:ConnectionStrings
site:example.com inurl:"credentials" ext:json OR ext:xml OR ext:txt
```

### A2. Backups, Dumps, Leftovers

```text
site:example.com ext:sql OR ext:dbf OR ext:mdb
site:example.com ext:sql intext:"INSERT INTO"
site:example.com ext:sql intext:"CREATE TABLE"
site:example.com ext:sql "DROP TABLE IF EXISTS"
site:example.com ext:bak OR ext:old OR ext:orig OR ext:save
site:example.com ext:swp OR ext:swo OR ext:tmp
site:example.com ext:~ OR ext:_old
site:example.com inurl:backup ext:zip OR ext:tar OR ext:gz OR ext:rar OR ext:7z
site:example.com inurl:dump
site:example.com inurl:"backup.sql"
site:example.com "index of" "backup"
site:example.com ext:tgz OR ext:tar.gz
site:example.com ext:sqlite OR ext:db
site:example.com ext:csv "password" OR "passwd"
site:example.com ext:txt intext:"password" inurl:backup
site:example.com inurl:"wp-config.php.bak"
site:example.com inurl:".env.bak" OR inurl:".env.old" OR inurl:".env.save"
site:example.com inurl:".env.local" OR inurl:".env.production" OR inurl:".env.dev"
```

### A3. Open Directories / Index Listings

```text
site:example.com intitle:"index of /"
site:example.com intitle:"index of" "parent directory"
site:example.com intitle:"index of" "last modified"
intitle:"index of" "example.com"
intitle:"index of" inurl:example.com "/backup"
intitle:"index of" "/uploads" site:example.com
intitle:"index of" "/files" site:example.com
intitle:"index of" "/private" site:example.com
intitle:"index of" "/admin" site:example.com
intitle:"index of" "/config" site:example.com
intitle:"index of" "/logs" site:example.com
intitle:"index of" "/db" OR "/database" site:example.com
intitle:"index of" "/.git" site:example.com
intitle:"index of" "/.ssh" site:example.com
intitle:"index of" "id_rsa" site:example.com
intitle:"index of" "credentials"
intitle:"index of" "secrets"
intitle:"index of" "node_modules" site:example.com
intitle:"index of" "vendor" site:example.com
intitle:"index of" ".bash_history"
intitle:"index of" "wp-content/uploads"
intitle:"index of" "*.sql" OR "*.bak" OR "*.zip"
intitle:"index of" "ftp"
```

### A4. Exposed VCS / Build / Dev Artifacts

```text
site:example.com inurl:".git/config"
site:example.com inurl:".git/HEAD"
site:example.com inurl:".git/logs/HEAD"
site:example.com inurl:".gitignore"
site:example.com inurl:".svn/wc.db" OR inurl:".svn/entries"
site:example.com inurl:".hg" OR inurl:".bzr"
site:example.com inurl:".DS_Store"
site:example.com inurl:"Thumbs.db"
site:example.com inurl:".gitlab-ci.yml"
site:example.com inurl:"Jenkinsfile"
site:example.com inurl:".travis.yml"
site:example.com inurl:".circleci/config.yml"
site:example.com inurl:"azure-pipelines.yml"
site:example.com inurl:".github/workflows" ext:yml
site:example.com inurl:"composer.lock" OR inurl:"composer.json"
site:example.com inurl:"package.json" intext:dependencies
site:example.com inurl:"yarn.lock" OR inurl:"package-lock.json"
site:example.com inurl:"Gemfile" OR inurl:"Gemfile.lock"
site:example.com inurl:"requirements.txt"
site:example.com inurl:"webpack.config.js"
```

### A5. Login / Admin / Panels

```text
site:example.com inurl:admin
site:example.com inurl:administrator
site:example.com inurl:login OR inurl:signin OR inurl:logon OR inurl:auth
site:example.com inurl:"/admin/login"
site:example.com inurl:wp-login.php OR inurl:wp-admin
site:example.com inurl:phpmyadmin OR intitle:phpMyAdmin
site:example.com inurl:adminer.php OR intitle:Adminer
site:example.com inurl:"/cpanel" OR inurl:":2083"
site:example.com inurl:"/webmail" OR inurl:roundcube OR inurl:squirrelmail
site:example.com intitle:"Dashboard" inurl:admin
site:example.com intitle:"Control Panel"
site:example.com intitle:"Sign In" intext:password
site:example.com inurl:"/manager/html"
site:example.com intitle:"Apache Tomcat" intext:"Manager"
site:example.com intitle:"Grafana"
site:example.com intitle:"Kibana"
site:example.com intitle:"Jenkins"
site:example.com intitle:"Portainer"
site:example.com intitle:"Jupyter Notebook"
site:example.com intitle:"GitLab" inurl:users/sign_in
site:example.com intitle:"Nexus Repository Manager"
site:example.com intitle:"Harbor" inurl:harbor
site:example.com intitle:"Argo CD"
site:example.com intitle:"Rancher"
site:example.com intitle:"pfSense" intext:Login
site:example.com intitle:"OPNsense"
site:example.com intitle:"Synology" "DiskStation"
site:example.com intitle:"QNAP" inurl:cgi-bin
site:example.com inurl:":8006" intitle:Proxmox
```

### A6. Key / Token Prefixes in Cleartext

```text
site:example.com intext:"AKIA"
site:example.com intext:"ASIA"
site:example.com intext:"AIza"
site:example.com intext:"ya29."
site:example.com intext:"sk_live_"
site:example.com intext:"pk_live_"
site:example.com intext:"rk_live_"
site:example.com intext:"xoxb-" OR intext:"xoxp-" OR intext:"xoxa-"
site:example.com intext:"ghp_" OR intext:"gho_" OR intext:"ghs_"
site:example.com intext:"glpat-"
site:example.com intext:"shpat_" OR intext:"shpss_"
site:example.com intext:"sq0atp-" OR intext:"sq0csp-"
site:example.com intext:"SG."
site:example.com intext:"key-" "mailgun"
site:example.com intext:"AC" "twilio" intext:"auth_token"
site:example.com intext:"eyJ" "alg" "typ"
site:example.com intext:"-----BEGIN RSA PRIVATE KEY-----"
site:example.com intext:"-----BEGIN OPENSSH PRIVATE KEY-----"
site:example.com intext:"-----BEGIN DSA PRIVATE KEY-----"
site:example.com intext:"-----BEGIN EC PRIVATE KEY-----"
site:example.com intext:"-----BEGIN PGP PRIVATE KEY BLOCK-----"
site:example.com intext:"client_secret" intext:"client_id"
site:example.com intext:"BEGIN CERTIFICATE" ext:pem OR ext:crt OR ext:key
```

### A7. Error Pages / Info Disclosure

```text
site:example.com intext:"sql syntax near"
site:example.com intext:"You have an error in your SQL syntax"
site:example.com intext:"Warning: mysql_" OR intext:"mysqli_"
site:example.com intext:"ORA-00933" OR intext:"ORA-01756"
site:example.com intext:"Microsoft OLE DB Provider for SQL Server"
site:example.com intext:"Unclosed quotation mark"
site:example.com intext:"Fatal error" intext:"on line"
site:example.com intext:"Notice: Undefined index"
site:example.com intext:"Call Stack" intext:"Memory"
site:example.com intext:"Traceback (most recent call last)"
site:example.com intext:"Whitelabel Error Page"
site:example.com intext:"Werkzeug Debugger"
site:example.com intext:"DEBUG = True" OR intext:"Django Version"
site:example.com intext:"RAILS_ENV" OR intext:"ActionController"
site:example.com inurl:phpinfo.php OR intitle:"phpinfo()"
site:example.com intext:"PHP Version" "Configuration"
site:example.com intext:"Server at" intext:"Port 80"
site:example.com intext:"X-Powered-By"
site:example.com intext:"AH00" "Apache"
```

### A8. Cloud Storage / S3 & Other Buckets

```text
site:s3.amazonaws.com "example"
site:s3.amazonaws.com "Example Corp"
site:s3.amazonaws.com intitle:"index of"
site:s3.amazonaws.com filetype:xls OR filetype:csv OR filetype:pdf "example"
site:s3.amazonaws.com inurl:backup
site:s3.amazonaws.com ext:sql OR ext:env OR ext:bak
site:s3-external-1.amazonaws.com "example"
site:s3-us-west-2.amazonaws.com "example"
site:s3-eu-west-1.amazonaws.com "example"
site:s3-ap-southeast-1.amazonaws.com "example"
site:s3.us-east-1.amazonaws.com "example"
site:s3.eu-central-1.amazonaws.com "example"
inurl:s3.amazonaws.com "example" intitle:"index"
inurl:".s3.amazonaws.com" "example"
inurl:"s3.amazonaws.com/example"
site:amazonaws.com inurl:".s3." "Example Corp"
site:storage.googleapis.com "example"
site:storage.googleapis.com intitle:"index of"
site:storage.googleapis.com ext:sql OR ext:csv OR ext:json "example"
site:firebasestorage.googleapis.com "example"
inurl:"firebaseio.com/.json"
site:firebaseio.com "example"
site:blob.core.windows.net "example"
site:blob.core.windows.net intitle:"index of"
site:file.core.windows.net "example"
site:queue.core.windows.net "example"
site:table.core.windows.net "example"
site:digitaloceanspaces.com "example"
site:digitaloceanspaces.com intitle:"index of"
site:r2.dev "example"
site:r2.cloudflarestorage.com "example"
site:cdn.example.com intitle:"index of"
site:appspot.com "Example Corp"
site:objects.githubusercontent.com "Example Corp"
site:cellar-c2.services.clever-cloud.com "example"
site:cos.ap-guangzhou.myqcloud.com "example"
site:oss-cn-hangzhou.aliyuncs.com "example"
site:wasabisys.com "example"
site:backblazeb2.com "example"
site:linodeobjects.com "example"
```

### A9. APIs / Docs / Debug Endpoints

```text
site:example.com inurl:swagger OR inurl:"swagger-ui"
site:example.com inurl:"api-docs" OR inurl:"openapi.json" OR inurl:"openapi.yaml"
site:example.com inurl:graphql OR inurl:graphiql OR inurl:playground
site:example.com inurl:"/v1/" OR inurl:"/api/v1"
site:example.com inurl:"/rest/" intext:json
site:example.com inurl:wsdl OR ext:wsdl
site:example.com inurl:actuator
site:example.com inurl:"actuator/health" OR inurl:"actuator/env"
site:example.com inurl:"/metrics"
site:example.com inurl:"/debug/pprof"
site:example.com inurl:"/.well-known/security.txt"
site:example.com inurl:"/server-status"
site:example.com inurl:"/server-info"
site:example.com inurl:"/status" intext:"uptime"
site:example.com inurl:"/_profiler"
site:example.com inurl:"/telescope"
site:example.com inurl:"/horizon"
site:example.com inurl:"/__debug__"
```

### A10. Dev / Staging / Subdomain Surface

```text
site:*.example.com -www
site:*.example.com -www -shop -blog
site:dev.example.com OR site:staging.example.com OR site:stage.example.com
site:test.example.com OR site:qa.example.com OR site:uat.example.com
site:beta.example.com OR site:demo.example.com OR site:sandbox.example.com
site:internal.example.com OR site:intranet.example.com OR site:corp.example.com
site:vpn.example.com OR site:remote.example.com OR site:portal.example.com
site:git.example.com OR site:gitlab.example.com OR site:jenkins.example.com
site:jira.example.com OR site:confluence.example.com OR site:wiki.example.com
site:admin.example.com OR site:dashboard.example.com OR site:panel.example.com
site:api.example.com OR site:api-dev.example.com OR site:apidocs.example.com
site:mail.example.com OR site:webmail.example.com OR site:smtp.example.com
site:files.example.com OR site:download.example.com OR site:ftp.example.com
site:status.example.com OR site:monitor.example.com OR site:grafana.example.com
site:example.com -site:www.example.com
```

For Cert Transparency in the browser, open this URL directly: `https://crt.sh/?q=%25.example.com` for all subdomains known to CT logs.

### A11. CMS-Specific

```text
site:example.com inurl:"wp-content/debug.log"
site:example.com inurl:"wp-content/uploads" ext:sql OR ext:zip
site:example.com inurl:"wp-json/wp/v2/users"
site:example.com inurl:"/?author=1"
site:example.com inurl:"/sites/default/files" "drupal"
site:example.com inurl:"CHANGELOG.txt" "drupal"
site:example.com inurl:"/administrator/" "Joomla"
site:example.com inurl:"configuration.php-dist"
site:example.com inurl:"/typo3conf/"
site:example.com inurl:"/magento_version"
site:example.com inurl:"/app/etc/local.xml"
site:example.com inurl:"/sitecore/"
site:example.com inurl:"/umbraco/"
```

### A12. Document Leakage (Technical)

```text
site:example.com filetype:pdf intext:"confidential"
site:example.com filetype:pdf intext:"internal use only"
site:example.com filetype:pdf intext:"do not distribute"
site:example.com filetype:pdf intext:"draft"
site:example.com filetype:xlsx OR filetype:xls intext:"internal"
site:example.com filetype:xlsx intext:"password" OR intext:"login"
site:example.com filetype:docx intext:"proprietary"
site:example.com filetype:pptx intext:"roadmap" OR intext:"strategy"
site:example.com filetype:csv intext:"@example.com"
site:example.com filetype:csv intext:"ssn" OR intext:"dob"
site:example.com filetype:txt intext:"username" intext:"password"
site:example.com filetype:rtf OR filetype:odt intext:confidential
site:example.com filetype:pdf intext:"network diagram"
site:example.com filetype:vsdx OR filetype:vsd
```

---

## PART B — THE HUMAN PART

### B1. Email & Account Enumeration

```text
"@example.com" -site:example.com
intext:"@example.com" filetype:xlsx OR filetype:csv OR filetype:pdf
"@example.com" site:linkedin.com
"@example.com" site:github.com
"@example.com" site:gitlab.com
"@example.com" site:stackoverflow.com OR site:stackexchange.com
"@example.com" site:pastebin.com OR site:rentry.co OR site:ghostbin.com
"@example.com" site:scribd.com OR site:slideshare.net
"@example.com" site:docs.google.com
"firstname.lastname@example.com"
"f.lastname@example.com" OR "flastname@example.com"
intext:"@example.com" intext:"password"
intext:"@example.com" "smtp" OR "imap"
"@example.com" filetype:log
"@example.com" "DKIM" OR "SPF" OR "dmarc"
```

### B2. Employee / Org Mapping

```text
site:linkedin.com/in "Example Corp"
site:linkedin.com/in "Example Corp" ("CISO" OR "Security" OR "IT")
site:linkedin.com/in "Example Corp" ("DevOps" OR "SRE" OR "Cloud")
site:linkedin.com/in "Example Corp" ("HR" OR "Recruiter" OR "Talent")
site:linkedin.com/in "Example Corp" ("Finance" OR "Accounts Payable")
site:linkedin.com/company "Example Corp"
site:x.com OR site:twitter.com "Example Corp"
site:github.com "Example Corp" OR "@example.com"
site:medium.com "Example Corp" engineering
site:dev.to "Example Corp"
site:reddit.com "Example Corp" ("works" OR "employee" OR "interview")
site:glassdoor.com "Example Corp"
site:xing.com "Example Corp"
site:kununu.com "Example Corp"
```

### B3. Resumes / CVs

```text
intext:"Example Corp" filetype:pdf ("resume" OR "curriculum vitae")
intext:"Example Corp" filetype:pdf ("Lebenslauf" OR "CV")
"@example.com" filetype:pdf resume
intitle:"resume" "Example Corp" filetype:doc OR filetype:docx OR filetype:pdf
filetype:pdf "Example Corp" ("AWS" OR "Kubernetes" OR "Active Directory")
intext:"worked at Example Corp" filetype:pdf
site:example.com filetype:pdf "references available"
```

### B4. Passive Breach / Paste / Leak Exposure

```text
site:pastebin.com "example.com"
site:pastebin.com "@example.com" password
site:rentry.co OR site:ghostbin.com OR site:dpaste.org "example.com"
site:throwbin.io OR site:controlc.com "example.com"
site:trello.com "Example Corp"
site:trello.com "example.com" (password OR token OR credentials)
site:scribd.com "Example Corp" confidential
site:slideshare.net "Example Corp" internal
site:anonfiles.com OR site:mega.nz "Example Corp"
"example.com" intext:"password" ext:txt
"example.com" "combolist" OR "combo list"
```

### B5. Phone / Contact / Addresses

```text
"@example.com" intext:"phone" OR intext:"tel" OR intext:"mobile"
site:example.com filetype:vcf
intext:"Example Corp" filetype:pdf ("Tel" OR "Phone" OR "Mobile")
"Example Corp" "contact" filetype:xlsx OR filetype:csv
site:example.com inurl:"contact" intext:"@example.com"
site:example.com intext:"reception" OR intext:"front desk" intext:phone
```

### B6. Social-Engineering Pretext Building

```text
site:example.com intext:"org chart" OR intext:"organizational chart"
site:example.com intext:"new hire" OR intext:"welcome to the team" OR intext:"onboarding"
site:example.com "press release" ("appointed" OR "joins" OR "promoted")
site:example.com filetype:pdf "employee handbook"
site:example.com intext:"badge" OR intext:"access card"
site:example.com intext:"VPN" OR intext:"remote access"
site:example.com intext:"help desk" OR intext:"service desk" OR intext:"IT support"
site:example.com intext:"reset password" OR intext:"forgot password"
site:example.com intext:"ticketing" OR intext:"ServiceNow" OR inurl:"servicenow.com"
site:example.com intext:"single sign-on" OR intext:"SSO" OR intext:"Okta" OR intext:"Azure AD"
site:example.com intext:"travel policy" OR intext:"expense report"
site:example.com intext:"supplier" OR intext:"vendor" "invoice"
site:example.com filetype:pdf "purchase order" OR "PO number"
```

### B7. Calendars / Meetings / Event Leaks

```text
site:example.com inurl:calendar
"example.com" inurl:"zoom.us/j"
"Example Corp" "zoom.us/j" OR "zoom.us/my"
"Example Corp" "teams.microsoft.com/l/meetup-join"
"Example Corp" calendly.com
"Example Corp" "meet.google.com"
site:docs.google.com "Example Corp"
site:sheets.google.com "Example Corp"
inurl:"/spreadsheets/d/" "Example Corp"
inurl:"docs.google.com/document/d" "Example Corp"
inurl:"/forms/d/e/" "Example Corp"
site:onedrive.live.com "Example Corp"
site:1drv.ms "Example Corp"
site:sharepoint.com "Example Corp"
site:notion.so "Example Corp"
site:airtable.com "Example Corp"
```

### B8. Repos & Code with Personal / Internal Info

```text
site:github.com "example.com" "password"
site:github.com "example.com" "BEGIN PRIVATE KEY"
site:github.com "example.com" "smtp" "pass"
site:github.com "@example.com" "todo" OR "fixme" OR "hack"
site:github.com "Example Corp" "internal" ".env"
site:gitlab.com "Example Corp"
site:bitbucket.org "Example Corp"
site:gist.github.com "example.com"
site:github.com "example.com" "api_key" OR "apikey"
site:github.com "example.com" "Authorization: Bearer"
```

### B9. Username Pivoting

```text
"jdoe" "Example Corp"
"jdoe" site:github.com OR site:twitter.com OR site:reddit.com OR site:keybase.io
"jdoe" site:gravatar.com
intext:"johndoe" site:github.com
"john.doe" "Example Corp" -site:linkedin.com
```

### B10. Geo / Physical / Brand Surface

```text
"Example Corp" site:instagram.com
"Example Corp" site:flickr.com
"Example Corp" "office" filetype:pdf "floor plan"
"Example Corp" intext:"loading dock" OR intext:"reception hours"
"Example Corp" site:foursquare.com OR site:yelp.com
"Example Corp" "datacenter" address
```

---

## PART C — Advanced Browser Techniques (2026)

### C1. Date-Bounding for Fresh Exposures (Google)

```text
site:example.com ext:env after:2026-01-01
site:example.com "index of" after:2026-03-01
site:pastebin.com "example.com" after:2026-05-01
```

### C2. Wildcard & Phrase Stacking (Yandex shines)

```text
site:example.com "password is *"
site:example.com "the * key is"
"* @example.com" "password"
```

### C3. Negative Filtering to Kill Noise

```text
site:example.com inurl:admin -inurl:wp-admin -intitle:blog
"@example.com" -site:linkedin.com -site:facebook.com -site:example.com
site:*.example.com -www -www2 -shop -support
```

### C4. Engine-Specific Special Dorks

Bing only:

```text
ip:203.0.113.10
ip:203.0.113.10 site:example.com
inbody:"password" site:example.com
feed:example.com
hasfeed:example.com
language:de site:example.com intext:vertraulich
```

Yandex only:

```text
host:example.com
rhost:com.example.*
mime:pdf site:example.com confidential
url:admin site:example.com
date:>20260101 site:example.com
```

DuckDuckGo:

```text
site:example.com filetype:env
"@example.com" -site:example.com
```

### C5. Same Dork, Five Engines

1. Google: maximum coverage, best operator combos.
2. Bing: ip:, feed:, inbody: find what Google drops.
3. Yandex: real wildcards, host:/rhost:, RU/CIS infra, image OSINT.
4. DuckDuckGo: different index source, less personalization.
5. Brave: independent index, good for fresh or small sites.

### C6. Browser-Only Subdomain Discovery

Open these URLs directly in the browser, no tools needed:

```text
https://crt.sh/?q=%25.example.com
https://web.archive.org/cdx/search/cdx?url=*.example.com&output=text&fl=original&collapse=urlkey
```

The Wayback CDX endpoint lists historical URLs and subdomains as plain text in the browser.

### C7. Wayback / Archive Dorking

Find archived, possibly removed sensitive pages:

```text
https://web.archive.org/web/*/example.com/*
https://web.archive.org/web/2023*/example.com/admin*
```

Useful for old .env or config files that are already gone from the live site.

---

## PART D — Operational Notes (Browser)

- Rate-limit yourself. Too many dorks too fast triggers CAPTCHAs or temporary blocks. Pause and switch engines.
- Logged in vs anonymous: being signed into Google gives personalized, filtered results. For recon, use incognito or stay logged out.
- Engine-hopping beats VPN-hopping. Try another engine before changing your IP.
- Date-bound with after: to find new leaks, which are the most valuable because they are not fixed yet.
- Stack operators: combine site: + inurl: + intext: + filetype: for surgical hits instead of broad lists.

