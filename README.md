# WebHackingNotes
1- INFORMATION GATHERING: Information gathering is a part of hunting security bugs.
Attack Surface Reconnaisance – Strategies and the Value of Standardization

***The Technology Stack: Identify the technologies used
- One of the first tasks I do when testing a new application is identify the
technologies being used. This includes, but isn’t limited to, frontend
JavaScript frameworks, server-side application frameworks, third-party
services, locally hosted files, remote files, and so on.
- Having the knowledge about the framework used to develop a website gives
you an advantage in identifying the vulnerabilities that may exist in the
unpatched versions.
- Look for what the underlying tech is. useful tool for this is nmap again & for web apps
specifically wappalyzer

***Identifying virtual hosts: Multiple websites are commonly deployed on the same physical server.
- The websites of many organizations are hosted by service providers using
shared resources. The sharing of IP addresses is one of the most useful and
cost-effective techniques used by them. You will often see a number of
domain names returned when you do a reverse DNS query for a specific IP
address. These websites use name-based virtual hosting, and they are
uniquely identified and differentiated from other websites hosted on the
same IP address by the host header value.
- The YouGetSignal (http://www.yougetsignal.com/) is a website that provides
a reverse IP lookup feature.

***Subdomain Enumeration:
- you can begin your recon by finding subdomains
using your VPS. The more subdomains you find, the more attack surface you’ll have.
- Finding subdomains of a website can land us in surprising
places. I remember a talk by Israeli security researcher, Nir Goldshlager, in which he
performed a subdomain enumeration scan on a Google service, out of the bunch of
subdomains he found there was one which ran a web application with a publicly
disclosed local file inclusion vulnerability.

***Port Scanning:
- After you’ve enumerated subdomains, you can start portscanning to identify more attack
surfaces, including running services.
- Utilize port scanning -Don’t look for just the normal 80,443 - run a port scan against all 65536
ports. You’ll be surprised what can be running on random high ports.
- The results of the portscan can also be indicative of a company’s overall security. For
example, a company that has closed all ports except 80 and 443 (common web ports for
hosting HTTP and HTTPS sites) is likely to be security conscious, while a company with a
lot of open ports open is likely the opposite and may have better potential for bounties.
- After identifying the open ports on the web server, you need to determine
the underlying operating system.
- Once the underlying operating system and open ports have been
determined, you need to identify the exact applications running on the open
ports. When scanning web servers, you need to analyze the flavor and
version of web service that is running on top of the operating system.

***Content Discovery: Discover hidden & default content
- Before we depart our tour of the many uses of Internet search engines, we want to make
note of one additional search-related issue that can greatly enhance the efficiency of
profiling. The robots.txt file contains a list of directories that search engines such as
Google are supposed to index or ignore.
- Sitemaps are an absurdly simple way of doing basic research with zero effort. Doing a little
URL hacking with the sitemap.xml slug will often return either an actual XML file
detailing the site's structure, or a Yoast-or-other-seo-plugin-supplied HTML page
documenting different areas of the site, with separate sitemaps for posts, pages, and so on.
- Map out the application looking for hidden directories, or forgotten things like /backup/
etc.
- There are a few different ways to approach content discovery. First, you can attempt to
discover files and directories by bruteforcing them.
- Fuzzing tools can be used to discover web content by trying different paths,
with URIs taken from giant wordlists, then analyzing the HTTP status codes of the
responses to discover hidden directories and files.
- CeWL is a custom wordlist generator made by Robin Hood. It basically spiders
the target site to a certain depth and then returns a list of words. This wordlist can
later be used as a dictionary to bruteforce web application logins, for example an
administrative portal.
- Parallel to brute-forcing for sensitive assets, spidering can help you get a picture of a site
that, without a sitemap, just brute-forcing itself can't provide.
- The web server may have directories for administrators, old versions of the 
site, backup directories, data directories, or other directories that 
are not referenced in any HTML code.
- Obtain listings of common fi le and directory names and common fi le
extensions. Add to these lists all the items actually observed within the
applications, and also items inferred from these. Try to understand the
naming conventions used by application developers. For example, if
there are pages called AddDocument.jsp and ViewDocument.jsp, there
may also be pages called EditDocument.jsp and RemoveDocument.jsp.
- Verify any potentially interesting fi ndings manually to eliminate any
false positives within the results.

***Consult Public Resources: Accumulating information about the target website from publicly
available resources
- When you need to go beyond file and directory bruteforcing, Google Dorking, can also provide
some interesting content discovery. Google Dorking can save you time, particularly when
you find URL parameters that are commonly associated with vulnerabilities such as url,
redirect_to, id, and so on.
- Search engines have always been a hacker’s best friend. It’s a good bet that at least one
of the major Internet search engines has indexed your target web application at least
once in the past.
- Beyond Google there are other search engines with a specific focus that can be invaluable
in finding specific information. Whether you want to find information on a person or
inquire about public records, chances are a specialized search engine has been made to
find what you desire.
- Perform searches on any names and e-mail addresses you have discovered
in the application’s content, such as contact information. Include
items not rendered on-screen, such as HTML comments. In addition to
web searches, perform news and group searches. Look for any technical
details posted to Internet forums regarding the target application and
its supporting infrastructure.
- Another approach to find interesting content is to check the company’s GitHub. You
may find open source repositories from the company or helpful information about the
technologies they use.
- Github is a treasure trove of amazing data. There have been a number of penetration
tests and Red Team assessments where we were able to get passwords, API keys, old
source code, internal hostnames/IPs, and more. These either led to a direct
compromise or assisted in another attack. What we see is that many developers either
push code to the wrong repo (sending it to their public repository instead of their
company’s private repository), or accidentally push sensitive material (like passwords)
and then try to remove it. One good thing with Github is that it tracks every time code
is modified or deleted.
- Shodan (https://www.shodan.io) is a great service that regularly scans the internet,
grabbing banners, ports, information about networks, and more.
- Censys continually monitors every reachable server and device on the Internet, so you
can search for and analyze them in real time. You will be able to understand your
network attack surface, discover new threats, and assess their global impact
[https://censys.io/].
- Utilize the waybackmachine for finding forgotten endpoints

***Identifying New Fuctionality:
- You can also discover new site functionality by tracking JavaScript files.
Focusing on JavaScript files is particularly powerful when a site relies on
frontend JavaScript frameworks to render its content. The application
will rely on having most of the HTTP endpoints a site uses included in
its JavaScript files.
- Paying for Access to New Functionality

***Source Code:
Source-code analysis is typically thought of as something that only takes place in a white
box, an internal testing scenario, either as part of an automated build chain or as a manual
review. But analyzing client-side code available to the browser is also an effective way of
looking for vulnerabilities as an outside researcher.
