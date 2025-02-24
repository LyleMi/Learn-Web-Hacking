Search engine utilization
========================================
Use search engines appropriately (Google/Bing/Yahoo/Baidu, etc.) to obtain more information about the target site.

Search engine processing flow
----------------------------------------
- Data preprocessing
- Length cutoff
-Case conversion
- Remove punctuation marks
- Simplified and traditional Chinese conversion
- Number normalization, Chinese numerals, Arabic numerals, Roman characters
- Synonyms rewrite
- Pinyin rewrite
- deal with
- Partial word
- Keyword extraction
- Illegal information filtering

Search Tips
----------------------------------------
- site:www.hao123.com
- Return to all content that this target site was crawled and included by search engines
- site:www.hao123.com keyword
- Return to all pages containing this keyword that are crawled and included by search engines
- Here you can set keywords as website background, management background, password modification, password recovery, etc.
-
- Return to all pages containing admin.php in the address of the target site. You can use admin.php/manage.php or other keywords to find key functional pages.
- link:www.hao123.com
- Return to all pages containing links to the target site, including their developers' personal blogs, development logs, or third-party companies, partners, etc. that open the site
- related:www.hao123.com
- Return to all pages that are "similar" to the target site, which may contain some general program information, etc.
- intitle:"500 Internal Server Error" "server at"
- Search for the page that was wrong
- inurl:"nph-proxy.cgi" "Start browsing"
- Find proxy server

In addition to the above keywords, there are allintile/allinurl/allintext/innchor/intext/filetype/info/numberange/cache, etc.

Wildcard
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``*`` represents a certain word
- OR or | stands for logic or
- Forced query before word ``+`` table
- The word prefixes the corresponding keywords in the table
- ``"`` emphasizes keywords

tips
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Query is case-insensitive
- Brackets will be ignored
- Search by default with and logic

Snapshot
----------------------------------------
Search engine snapshots often contain some key information. For example, program error information may leak the specific path of the website, or some snapshots will save some test information. For example, when a website develops a background function module, The search engine has not added permission authentication to all pages, and the snapshot was taken by the search engine. Even if the website later added permission authentication, the search engine's snapshot will still retain this information.

In addition, there are special site snapshots that provide snapshot functions, such as Wayback Machine and `Archive.org <https://archive.org/>`_, etc.

Girub
----------------------------------------
In Github, there may be source code leakage, AccessKey leakage, password, server configuration leakage, etc. Common search techniques include:

- ``@example.com password/pass/pwd/secret/credentials/token``
- ``@example.com username/user/key/login/ftp/``
- ``@example.com config/ftp/smtp/pop``
- ``@example.com security_credentials/connetionstring``
- ``@example.com JDBC/ssh2_auth_password/send_keys``
