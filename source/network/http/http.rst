HTTP standard
========================================

Message format
----------------------------------------

Request message format
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
::

    <method><request-URL><version>
    <headers>

    <entity-body>

Response message format
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
::

    <version><status><reason-phrase>
    <headers>

    <entity-body>

Field explanation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- method
    - HTTP verb
    - Common methods: HEAD/GET/POST/PUT/DELETE/PATCH/OPTIONS/TRACE
    -Extension methods: LOCK/MKCOL/COPY/MOVE
- version
    - HTTP version used by the message
    - The format is HTTP/<major>.<minor>
- url
    - ``<scheme>://<user>:<password>@<host>:<port>/<path>;<params>?<query>#<frag>``

Request header list
----------------------------------------
- Accept
    - Specify the content types that the client can receive
    - Accept: text/plain, text/html
- Accept-Charset
    - The character encoding set that the browser can accept
    - Accept-Charset: iso-8859-5
- Accept-Encoding
    - Specify the compression encoding type of content returned by the web server that the browser can support
    - Accept-Encoding: compress, gzip
- Accept-Language
    - Languages ​​accepted by the browser
    - Accept-Language: en,zh
- Accept-Ranges
    - You can request one or more sub-range fields of the web page entity
    - Accept-Ranges: bytes
- Authorization
    - Authorization certificate for HTTP authorization
    - Authorization: Basic QWxhZGRpbjpvcGVuIHNlc2FtZQ==
- Cache-Control
    - Specify the caching mechanism followed by requests and responses Cache-Control: no-cache
- Connection
    - Indicates whether a persistent connection is required // HTTP 1.1 uses persistent connections by default
    - Connection: close
- Cookie
    - When an HTTP request is sent, all cookie values ​​stored in the requested domain name will be sent to the web server.
    - Cookie: role=admin;ssid=1
- Content-Length
    - Requested content length
    - Content-Length: 348
- Content-Type
    - The requested MIME information corresponding to the entity
    - Content-Type: application/x-www-form-urlencoded
- Date
    - The date and time the request was sent
    - Date: Tue, 15 Nov 2010 08:12:31 GMT
- Expect
    - Request specific server behavior
    - Expect: 100-continue
- From
    - Email of the user making the request
    - From: user@email.com
- Host
    -Specify the domain name and port number of the requested server
    - Host: www.github.com
- If-Match
    - Valid only if the request content matches the entity
    - If-Match: "737060cd8c284d8af7ad3082f209582d"
- If-Modified-Since
    - If the requested part is modified after the specified time, the request is successful. If it is not modified, a 304 code is returned.
    - If-Modified-Since: Sat, 29 Oct 2018 19:43:31 GMT
- If-None-Match
    - If the content has not changed, a 304 code is returned. The parameter is the Etag previously sent by the server. Compare it with the Etag responded by the server to determine whether it has changed.
    - If-None-Match: "737060cd8c284d8af7ad3082f209582d"
- If-Range
    - If the entity has not changed, the server sends the client's missing parts, otherwise the entire entity is sent. The parameter is also Etag
    - If-Range: "737060cd8c284d8af7ad3082f209582d"
- If-Unmodified-Since
    - The request succeeds only if the entity has not been modified after the specified time
    - If-Unmodified-Since: Sat, 29 Oct 2010 19:43:31 GMT
- Max-Forwards
    - Limit the time that information is sent through proxies and gateways
    - Max-Forwards: 10
- Pragma
    - Used to contain implementation-specific instructions
    - Pragma: no-cache
- Proxy-Authorization
    - Authorization certificate to connect to the agent
    - Proxy-Authorization: Basic QWxhZGRpbjpvcGVuIHNlc2FtZQ==
- Range
    - Request only a part of the entity, specify the range
    - Range: bytes=500-999
- Referer
    - The address of the previous web page, followed by the current requested web page, that is, the origin
    - Referer: http://www.zcmhi.com/archives/71.html
- TE
    - The client is willing to accept the transfer encoding and notify the server to accept the tail plus header information.
    - TE: trailers,deflate;q=0.5
- Upgrade
    - Specify a transport protocol to the server for conversion (if supported)
    - Upgrade: HTTP/2.0, SHTTP/1.3, IRC/6.9, RTA/x11
- User-Agent
    - The content of User-Agent contains information about the user who made the request
    - User-Agent: Mozilla/5.0 (Linux; X11)
- Via
    - Notify intermediate gateway or proxy server address, communication protocol
    - Via: 1.0 fred, 1.1 nowhere.com (Apache/1.1)
- Warning
    - Warning information about message entities
    - Warn: 199 Miscellaneous warning

Response header list
----------------------------------------
- Accept-Ranges
    - Indicates whether the server supports the specified range request and what type of segmented request
    - Accept-Ranges: bytes
- Access-Control-Allow-Origin
    - Configure domains with permission to access resources
    - Access-Control-Allow-Origin: <origin>|*
- Age
    - Estimated time (in seconds, non-negative) from origin server to proxy cache formation
    - Age: 12
- Allow
    - A valid request behavior for a certain network resource. If it is not allowed, 405 will be returned.
    - Allow: GET, HEAD
- Cache-Control
    - Tell all caching mechanisms whether they can be cached and of what type
    - Cache-Control: no-cache
- Content-Encoding
    - The returned content compression encoding type supported by the web server.
    - Content-Encoding: gzip
- Content-Language
    - The language of the response body
    - Content-Language: en,zh
- Content-Length
    - The length of the response body
    - Content-Length: 348
- Content-Location
    - Request an alternative address for the resource
    - Content-Location: /index.htm
- Content-MD5
    - Returns the MD5 check value of the resource
    - Content-MD5: Q2hlY2sgSW50ZWdyaXR5IQ==
- Content-Range
    - The byte position of this part in the entire return body
    - Content-Range: bytes 21010-47021/47022
- Content-Type
    - Returns the MIME type of the content
    - Content-Type: text/html; charset=utf-8
- Date
    - The time the original server message was sent
    - Date: Tue, 15 Nov 2010 08:12:31 GMT
- ETag
    - The current value of the entity tag of the request variable
    - ETag: "737060cd8c284d8af7ad3082f209582d"
- Expires
    - The date and time the response expires
    - Expires: Thu, 01 Dec 2010 16:00:00 GMT
- Last-Modified
    - The last modification time of the requested resource
    - Last-Modified: Tue, 15 Nov 2010 12:45:26 GMT
- Location
    - Used to redirect the recipient to the location of a non-requested URL to complete the request or identify a new resource
    - Location: http://www.zcmhi.com/archives/94.html
- Pragma
    - Includes implementation-specific directives, which can be applied to any receiver in the response chain
    - Pragma: no-cache
- Proxy-Authenticate
    - It indicates the authentication scheme and parameters that can be applied to the proxy on that URL
    - Proxy-Authenticate: Basic
- Refresh
    - Applies to redirect or a new resource is created, redirect after 5 seconds (proposed by Netscape, supported by most browsers)
    - Refresh: 5; url=http://www.zcmhi.com/archives/94.html
- Retry-After
    - If the entity is temporarily unavailable, notify the client to try again after the specified time
    - Retry-After: 120
- Server
    - web server software name
    - Server: Apache/1.3.27 (Unix) (Red-Hat/Linux)
- Set-Cookie
    - Set Http Cookie Set-Cookie: UserID=JohnDoe; Max-Age=3600; Version=1
- Strict-Transport-Security
    - Set the browser to force HTTPS access
    - max-age: HTTPS requests are used to access the corresponding domain name within x seconds.
    - includeSubDomains: The subdomain name of the website also enables the rule
    - Strict-Transport-Security: max-age=1000; includeSubDomains
- Trailer
    - Indicates that header fields are present at the end of chunked transfer encoding Trailer: Max-Forwards
- Transfer-Encoding
    - File transfer encoding
    - Transfer-Encoding:chunked
- Vary
    - Tells the downstream proxy whether to use a cached response or request from the origin server
    - Vary: *
- Via
    - Tell the proxy where the client response is sent through
    - Via: 1.0 fred, 1.1 nowhere.com (Apache/1.1)
- Warning
    - Warn about possible problems with entities
    - Warning: 199 Miscellaneous warning
- WWW-Authenticate
    - Indicates the authorization scheme that the client requesting entity should use
    - WWW-Authenticate: Basic
- X-Content-Type-Options
    - Configure to disable MIME type sniffing
    - X-Content-Type-Options: nosniff
- X-Frame-Options
    - Configure whether the page can appear in <frame>, <iframe>, <embed>, <object> and other tags to prevent click hijacking
    - X-Frame-Options: deny
- X-XSS-Protection
    - Configure XSS protection mechanism
    - X-XSS-Protection: 1; mode=block

HTTP status return code 1xx (provisional response)
----------------------------------------
A status code that indicates a provisional response and requires the requestor to continue performing operations.

=====     ========    ======================================================================
Code Code Description
=====     ========    ======================================================================
100 Continue The server returns this code to indicate that it has received the first part of the request and is waiting for the remainder.
101 Switch protocol. The requester has asked the server to switch protocols. The server has confirmed and is ready to switch.
=====     ========    ======================================================================

HTTP status return code 2xx (success)
----------------------------------------
A status code indicating that the request was successfully processed.

=====     ==========    ======================================================================
Code Code Description
=====     ==========    ======================================================================
200 Success The server successfully processed the request. Typically, this means that the server served the requested web page
201 Created The request was successful and the server created a new resource.
202 Accepted The server has accepted the request but has not yet processed it.
203 Unauthorized Information The server successfully processed the request, but the returned information may have come from another source.
204 No Content The server successfully processed the request but did not return any content.
205 Reset content The server successfully processed the request but did not return any content.
206 Partial Content The server successfully processed part of the GET request.
=====     ==========    ======================================================================

HTTP status return code 3xx (redirect)
----------------------------------------
Indicates that further action is required to complete the request. Typically, these status codes are used for redirects.

=====     ============    ======================================================================
Code Code Description
=====     ============    ======================================================================
300+ Options The server can perform a variety of operations in response to a request. The server can select an action based on the requester (user agent) or provide a list of actions for the requester to choose from.
301 Moved Permanently The requested web page has been permanently moved to a new location. When the server returns this response (in response to a GET or HEAD request), it automatically forwards the requester to the new location.
302 Temporary Move The server is currently responding to the request from a page in a different location, but the requester should continue to use the original location for future requests.
303 View Other Locations The server returns this code when the requester should use separate GET requests to retrieve a response for a different location.
304 Not Modified The requested web page has not been modified since the last request. When the server returns this response, no web page content is returned.
305 Using Proxy The requester can only access the requested web page using a proxy. If the server returns this response, it also indicates that the requester should use a proxy.
307 Temporary Redirect The server is currently responding to the request from a web page in a different location, but the requester should continue to use the original location for future requests.
=====     ============    ======================================================================

HTTP status return code 4xx (request error)
----------------------------------------
These status codes indicate that the request may have gone wrong, preventing the server from processing it.

=====     ==================    ======================================================================
Code Code Description
=====     ==================    ======================================================================
400 Bad Request The server does not understand the syntax of the request.
401 Unauthorized The request requires authentication. For web pages that require login, the server may return this response.
403 Forbidden The server refused the request.
404 Not Found The server cannot find the requested web page.
405 Method Disabled Disables the method specified in the request.
406 Not Accepted Unable to respond to the requested web page with the requested content attributes.
407 Proxy Authorization Required This status code is similar to 401 (Not Authorized), but specifies that the requester should be authorized to use the proxy.
408 Request Timeout A timeout occurred while the server was waiting for a request.
409 Conflict The server encountered a conflict while completing the request. The server MUST include information about the conflict in the response.
410 Deleted The server returns this response if the requested resource has been permanently deleted.
411 Valid length required The server does not accept requests without a valid content-length header field.
412 Precondition not met The server did not meet one of the preconditions set by the requester in the request.
413 The request entity is too large. The server cannot process the request because the request entity is too large and exceeds the server's processing capabilities.
414 Requested URI too long The requested URI (usually a URL) is too long and cannot be processed by the server.
415 Unsupported Media Type The requested format is not supported by the requested page.
416 Requested scope does not meet requirements The server returns this status code if the page cannot provide the requested scope.
417 Expectation Not Met The server did not meet the requirements for the "Expect" request header field.
=====     ==================    ======================================================================

HTTP status return code 5xx (server error)
----------------------------------------
These status codes indicate that an internal error occurred while the server was trying to process the request. These errors may be errors on the server itself rather than an error in the request.

=====     ==================    ======================================================================
Code Code Description
=====     ==================    ======================================================================
500 Internal Server Error The server encountered an error and was unable to complete the request.
501 Not yet implemented The server does not have the functionality to complete the request. For example, this code may be returned when the server does not recognize the request method.
502 Bad Gateway The server, acting as a gateway or proxy, received an invalid response from an upstream server.
503 Service Unavailable The server is currently unavailable (due to overload or downtime for maintenance). Usually, this is a temporary state.
504 Gateway Timeout The server acted as a gateway or proxy, but did not receive the request from the upstream server in time.
505 HTTP version not supported The server does not support the HTTP protocol version used in the request.
=====     ==================    ======================================================================
