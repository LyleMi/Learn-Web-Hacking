Search engine utilization
========================================
Appropriate use of search engines (Google/Bing/Yahoo/Baidu, etc.) can obtain more information about the target site.

Search engine processing flow
----------------------------------------
- Data preprocessing
    - Length truncation
    - Case conversion
    - Remove punctuation marks
    - Conversion between Simplified and Traditional Chinese
    - Number normalization, Chinese numerals, Arabic numerals, Roman characters
    - Synonym rewriting
    - Pinyin rewritten
- deal with
    - participle
    - Keyword extraction
    - Illegal information filtering

Search skills
----------------------------------------
- site:www.hao123.com
    - Return all the content of this target site that is crawled and included by search engines
- site:www.hao123.com keyword
    - Return all pages containing this keyword that are crawled and included by search engines on this target site
    - Here you can set keywords as website backend, management backend, password modification, password retrieval, etc.
- site:www.hao123.com inurl:admin.php
    - Return all pages containing admin.php in the address of the target site. You can use admin.php/manage.php or other keywords to find key function pages.
- link:www.hao123.com
    - Returns all pages containing links to the target site, including its developer's personal blog, development log, or third-party companies, partners, etc. that open this site
- related:www.hao123.com
    - Returns all pages "similar" to the target site, which may contain information about some common programs, etc.
- intitle:"500 Internal Server Error" "server at"
    - Search for error pages
- inurl:"nph-proxy.cgi" "Start browsing"
    - Find proxy servers

In addition to the above keywords, there are also allintile/allinurl/allintext/inanchor/intext/filetype/info/numberange/cache, etc.

wildcard
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``*`` represents a certain word
- OR or | stands for logical OR
- Words preceded by ``+`` table forced query
- Words preceded by ``-`` exclude corresponding keywords
- ``"`` emphasize keywords

tips
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
-Query is not case sensitive
- brackets are ignored
- Search using and logic by default

Snapshot
----------------------------------------
Search engine snapshots also often contain some key information. For example, program error information may reveal the specific path of the website, or some snapshots may save some test information for testing. For example, when a website develops a backend function module, permission authentication has not been added to all pages. At this time, the snapshot is captured by the search engine. Even if the website later adds permission authentication, the search engine snapshot will still retain this information.

There are also specialized site snapshots that provide snapshot functions, such as Wayback Machine and `Archive.org <https://archive.org/>`_, etc.

Github
----------------------------------------
In Github, there may be source code leaks, AccessKey leaks, passwords, server configuration leaks, etc. Common search techniques include:

- ``@example.com password/pass/pwd/secret/credentials/token``
- ``@example.com username/user/key/login/ftp/``
- ``@example.com config/ftp/smtp/pop``
- ``@example.com security_credentials/connetionstring``
- ``@example.com JDBC/ssh2_auth_password/send_keys``
