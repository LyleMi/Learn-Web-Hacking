# English Translation Progress Log

This local note tracks translation batches after the initial English i18n
infrastructure was set up. It complements `english-version-plan.md`; keep this
file focused on current progress and near-term commit boundaries.

## Working Model

- The Chinese `source/` tree remains the canonical document structure.
- English translation is maintained in `locale/en/LC_MESSAGES/**/*.po`.
- Each batch should keep a narrow ownership boundary so it can be reviewed,
  built, and committed independently.
- Prefer one commit per coherent topic area, for example `auth/`, `info/`, or
  `cloud/docker/`.
- After each batch, run at least `make html-en`; run `make html-zh` when the
  build infrastructure or shared source settings change.

## Current Batch

Started on 2026-06-17.

| Area | Write Scope | Status | Notes |
| --- | --- | --- | --- |
| Authentication Mechanisms | `locale/en/LC_MESSAGES/auth/*.po` | Completed | Filled OAuth and NTLM pages; the remaining auth files already had no empty body `msgstr` entries. |
| Docker Security | `locale/en/LC_MESSAGES/cloud/docker/*.po` | Completed | Translated container basics, attack, identification, image, reference, hardening, and virtualization pages. |
| Information Gathering | `locale/en/LC_MESSAGES/info/*.po` | Completed | Translated domain, port, search engine, site, network, social, and reference pages. |
| Domain Name System | `locale/en/LC_MESSAGES/network/domain/*.po` | Completed | Translated DNS basics, attacks, organizations, RDAP, references, encryption schemes, exploitation, and terminology pages. |
| Kubernetes Security | `locale/en/LC_MESSAGES/cloud/k8s/*.po` | Completed | Translated Kubernetes concepts, references, and security pages; the index page already had no empty body `msgstr` entries. |
| Cloud Security Top-Level Pages | `locale/en/LC_MESSAGES/cloud/{history,oci,ref}.po` | Completed | Translated the cloud history, OCI/container standards, and cloud references pages. |
| SSH References and CVEs | `locale/en/LC_MESSAGES/network/ssh/{cve,ref}.po` | Completed | Translated SSH CVE notes and reference links; the index page already had no body `msgstr` issues. |
| SQL Injection Fuzzing | `locale/en/LC_MESSAGES/vuln/sql/fuzz.po` | Completed | Translated injection detection and SQL fuzzing payload notes, preserving payload syntax. |
| Network Protocol Pages | `locale/en/LC_MESSAGES/network/{basic,dhcp,ipsec,mail,route,ssl,tcp,udp,wifi}.po` | Completed | Translated the remaining top-level network protocol pages outside the already completed HTTP, DNS, and SSH subsections. |
| Common Vulnerability Pages | `locale/en/LC_MESSAGES/vuln/{cmdinjection,config,csrf,fileinclude,fileread,fileupload,httpSmuggling,pathtraversal,xpath,xxe}.po` and `locale/en/LC_MESSAGES/vuln/middleware/{apache,iis,nginx}.po` | Completed | Translated common vulnerability and middleware pages, preserving payloads, code snippets, and reference links. |

## Current Batch Verification

- `git diff --check`
- `python -msphinx -E -b html -D language=en source build\html\en`
- `rg -n "^#, fuzzy" locale\en\LC_MESSAGES\auth locale\en\LC_MESSAGES\cloud\docker locale\en\LC_MESSAGES\info locale\en\LC_MESSAGES\network\domain locale\en\LC_MESSAGES\cloud\k8s`
- `rg -n "^msgstr .*\p{Han}" locale\en\LC_MESSAGES\auth locale\en\LC_MESSAGES\cloud\docker locale\en\LC_MESSAGES\info locale\en\LC_MESSAGES\network\domain locale\en\LC_MESSAGES\cloud\k8s`
- Babel parse plus empty/fuzzy/Han-in-`msgstr` checks for:
  `locale/en/LC_MESSAGES/cloud/{history,oci,ref}.po`,
  `locale/en/LC_MESSAGES/network/ssh/{cve,ref}.po`, and
  `locale/en/LC_MESSAGES/vuln/sql/fuzz.po`
- Babel parse plus empty/fuzzy/Han-in-`msgstr` checks for:
  `locale/en/LC_MESSAGES/network/{basic,dhcp,ipsec,mail,route,ssl,tcp,udp,wifi}.po`
  and
  `locale/en/LC_MESSAGES/vuln/{cmdinjection,config,csrf,fileinclude,fileread,fileupload,httpSmuggling,pathtraversal,xpath,xxe}.po`
  plus `locale/en/LC_MESSAGES/vuln/middleware/{apache,iis,nginx}.po`

## Review Checklist

- Preserve `msgid` exactly; only edit `msgstr`.
- Preserve code blocks, inline literals, commands, URLs, payloads, paths, and
  protocol tokens unless the surrounding prose needs explanation.
- Keep acronyms such as SQL, XSS, CSRF, SSRF, XXE, JWT, OAuth, SAML, SCRAM,
  NTLM, SSO, OSINT, WHOIS, CDN, ASN, and WAF uppercase.
- Use Title Case for page titles and section headings.
- Remove no existing translations unless correcting a clear mistranslation.
- Build the English HTML before committing.

## Next Candidates

- Remaining `network/*.po` protocol pages outside `network/domain/` and
  `network/ssh/`.
- Remaining `vuln/*.po` pages outside the already translated SQL/XSS subsets.
- `network/http/http.po`, which is the only untranslated page left in the
  otherwise translated HTTP subsection.
