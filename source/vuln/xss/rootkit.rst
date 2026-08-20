persistence
========================================

Based on storage
----------------------------------------
Sometimes websites store information in Cookies or localStorage, and because this data is usually actively stored by the website, many times the data retrieved from Cookies or localStorage is not filtered, and is directly retrieved and displayed on the page. Even when data in JSON format is stored, some sites have calls such as ``eval(data)``. Therefore, when there is an XSS, the payload can be written into it and triggered under the corresponding conditions.

Under some conditions, this exploit may cause problems due to some special characters, which can be bypassed using ``String.fromCharCode``.

Service Worker
----------------------------------------
Service Worker can intercept http requests and play a role similar to a local proxy. Therefore, Service Worker can be used to hook some requests and return attack codes in the requests to achieve the purpose of persistent attacks.

In Chrome, you can view the status of Service Worker through ``chrome://inspect/#service-workers`` and stop it.

AppCache
----------------------------------------
In a controllable network environment (public wifi), you can use the AppCache mechanism to forcefully store some payloads. If they are not cleared, the corresponding payloads will always exist when the user accesses the site.
