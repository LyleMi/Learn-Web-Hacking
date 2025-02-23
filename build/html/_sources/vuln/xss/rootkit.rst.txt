Endurance
========================================

Based on storage
----------------------------------------
Sometimes the website will store information in a cookie or localStorage. Because these data are usually stored actively by the website, many times the data retrieved from the cookie or localStorage is not filtered, and it will be directly taken out and displayed on the page, or even stored. When using JSON format data, some sites have calls such as ``eval(data)``. Therefore, when there is an XSS, the payload can be written into it and triggered under the corresponding conditions.

Under some conditions, this utilization may cause problems due to some special characters, and you can use ``String.fromCharCode`` to bypass it.

Service Worker
----------------------------------------
Service Worker can intercept http requests and play a role similar to a local proxy. Therefore, you can use Service Worker Hook to return attack code in the request to achieve the purpose of persistent attacks.

In Chrome, you can view the status of the Service Worker through ``chrome://inspect/#service-workers`` and stop it.

AppCache
----------------------------------------
In a controllable network environment (public wifi), you can use the AppCache mechanism to force storage of some payloads. If it is not cleared, the corresponding payload will always exist when the user accesses the site.
