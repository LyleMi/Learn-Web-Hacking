HTTP Standard
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
- HTTP verbs
- Common Methods: HEAD/GET/POST/PUT/DELETE/PATCH/OPTIONS/TRACE
- Extension method: LOCK/MKCOL/COPY/MOVE
- version
- HTTP version used by the packet
- Format is HTTP/<major>.<minor>
- url
- ``<scheme>://<user>:<password>@<host>:<port>/<path>;<params>?<query>#<frag>``

Request header list
----------------------------------------
- Accept
- Specify the type of content that the client can receive
- Accept: text/plain, text/html
- Accept-Charset
- A set of characters that are acceptable to the browser
- Accept-Charset: iso-8859-5
- Accept-Encoding
- Specify the type of web server return content compression encoding that the browser can support
- Accept-Encoding: compress, gzip
- Accept-Language
- Browser acceptable language
- Accept-Language: en,zh
- Accept-Ranges
- One or more sub-range fields of a web entity can be requested
- Accept-Ranges: bytes
- Authorization
- Authorization certificate for HTTP authorization
- Authorization: Basic QWxhZGRpbjpvcGVuIHNlc2FtZQ==
- Cache-Control
- Specify the caching mechanism to which requests and responses follow Cache-Control: no-cache
- Connection
- Indicates whether a persistent connection is required // HTTP 1.1 defaults to perform persistent connections
- Connection: close
- Cookie
- When an HTTP request is sent, all cookie values stored under the request domain name will be sent to the web server together
- Cookie: role=admin;ssid=1
- Content-Length
- Requested content length
- Content-Length: 348
- Content-Type
- Requested MIME information corresponding to the entity
- Content-Type: application/x-www-form-urlencoded
- Date
- Date and time of requesting send
- Data: TUE, 15 Nov 2010 08:12:31 GMT
- Expect
- The specific server behavior requested
- Expect: 100-continue
- From
- Email of the requested user
- From: user@email.com
- Host
- Specify the domain name and port number of the requested server
- Host: www.github.com
- If-Match
- Only if the requested content matches the entity is valid
- If-Match: "737060cd8c284d8af7ad3082f209582d"
- If-Modified-Since
- If the requested part is modified after the specified time, the request is successful, and if it is not modified, the 304 code will be returned
- If-Modified-Since: Sat, 29 Oct 2018 19:43:31 GMT
- If-None-Match
- If the content has not changed, return 304 code, the parameter is the Etag sent by the server, and compare it with the Etag responded by the server to determine whether it has changed.
- If-None-Match: "737060cd8c284d8af7ad3082f209582d"
- If-Range
- If the entity has not changed, the server sends the missing part of the client, otherwise the entire entity is sent. The parameter is also Etag
- If-Range: "737060cd8c284d8af7ad3082f209582d"
- If-Unmodified-Since
- Request succeeds only if the entity has not been modified after the specified time
- If-Unmodified-Since: Sat, 29 Oct 2010 19:43:31 GMT
- Max-Forwards
- Limit the time when information is transmitted through the proxy and gateway
- Max-Forwards: 10
- Pragma
- Used to include implementation specific instructions
- Pragma: no-cache
- Proxy-Authorization
- Certificate of authorization to the proxy
- Proxy-Authorization: Basic QWxhZGRpbjpvcGVuIHNlc2FtZQ==
- Range
- Only request part of the entity, specify the scope
- Range: bytes=500-999
- referring
- The address of the previous web page, the current requested web page is immediately followed, that is, the origin
- Refer: http://www.zcmhi.com/archives/71.html
- the
- The client is willing to accept the transmission code and notify the server to accept the end-top information
- TE: trailers,deflate;q=0.5
- Upgrade
- Specify some transport protocol to the server for conversion (if supported)
- Upgrade: HTTP/2.0, SHTTP/1.3, IRC/6.9, RTA/x11
- User-Agent
- The content of User-Agent contains user information that issued the request
- User-Agent: Mozilla/5.0 (Linux; X11)
- Via
- Notify the intermediate gateway or proxy server address, communication protocol
- Via: 1.0 fred, 1.1 nowhere.com (Apache/1.1)
- Warning
- Warning information about the message entity
- Warn: 199 Miscellaneous warning

Response header list
----------------------------------------
- Accept-Ranges
- Indicates whether the server supports specified range requests and which type of segment requests
- Accept-Ranges: bytes
- Access-Control-Allow-Origin
- Configure domains with permission to access resources
- Access-Control-Allow-Origin: <origin>|*
- Age
- Estimated time (in seconds, non-negative) from the origin server to the proxy cache formation
- Age: 12
- Allow
- If valid request behavior for a certain network resource, if not allowed, return 405
- Allow: GET, HEAD
- Cache-Control
- Tell all cache mechanisms whether and which type
-Cache-Control: No-Cache
- Content-Encoding
- The web server supports the return content compression encoding type.
- Content-Encoding: gzip
- Content-Language
- Language of the response body
- Content-Language: en,zh
- Content-Length
- Length of the response body
- Content-Length: 348
- Content-Location
- Another alternative address to request a resource to replace
- Content-Location: /index.htm
- Content-MD5
- Return the MD5 check value of the resource
- Content-MD5: Q2hlY2sgSW50ZWdyaXR5IQ==
- Content-Range
- Byte position of this part in the entire return body
- Content-Range: bytes 21010-47021/47022
- Content-Type
- Return the MIME type of content
- Content-Type: text/html; charset=utf-8
- Date
- Time of the origin server message
- Data: TUE, 15 Nov 2010 08:12:31 GMT
- Etag
- The current value of the entity label of the request variable
Attj: “737060 Sadda, 4 Dahda 082, 09582 D”
- Expires
- Response expiration date and time
- Expires: Thu, 01 Dec 2010 16:00:00 GMT
- Last-Modified
- Last modification time for requesting resources
- Last-Modified: Tue, 15 Nov 2010 12:45:26 GMT
- Location
- Used to redirect the receiver to the location of the non-requested URL to complete the request or identify a new resource
- Location: http://www.zcmhi.com/archives/94.html
- Pragma
- Includes implementation specific instructions that can be applied to any receiver on the response chain
- Pragma: no-cache
- Proxy-Authenticate
- It indicates the authentication scheme and the parameters on that URL that can be applied to the proxy
- Proxy-Authenticate: Basic
- Refresh
- Apply for redirection or a new resource is created, redirected after 5 seconds (proposed by Netscape, supported by most browsers)
- Refresh: 5; url=http://www.zcmhi.com/archives/94.html
- Retry-After
- If the entity is temporarily undesirable, notify the client to try again after the specified time
- Retry-After: 120
- Server
- Web server software name
- Server: Apache/1.3.27 (Unix) (Red-Hat/Linux)
- Set-Cookie
- Set Http Cookie Set-Cookie: UserID=JohnDoe; Max-Age=3600; Version=1
- Strict-Transport-Security
- Set browser to force HTTPS access
- max-age: In x seconds, accessing the corresponding domain name uses HTTPS requests.
- includeSubDomains: The subdomains of the website also enables rules
- Strict-Transport-Security: max-age=1000; includeSubDomains
- Trailer
- Indicates that the header field exists at the tail of the block transmission encoding Trailer: Max-Forwards
- Transfer-Encoding
- File transfer encoding
- Transfer-Encoding:chunked
- Vary
- Tell the downstream agent whether to use cached responses or request from the original server
- Vary: *
- Via
- Tell the proxy client where the response is sent
- Via: 1.0 fred, 1.1 nowhere.com (Apache/1.1)
- Warning
- Warn of possible problems in the entity
- Warning: 199 Miscellaneous warning
- WWW-Authenticate
- Indicates that the authorization scheme that the client requesting entity should use
- WWW-Authenticate: Basic
- X-Content-Type-Options
- Configure sniffing of MIME type
- X-Content-Type-Options: nosniff
- X-Frame-Options
- Whether the configuration page can appear in <frame>, <iframe>, <embed>, <object> and other tags to prevent click hijacking
- X-Frame-Options: deny
- X-XSS-Protection
- Configure XSS protection mechanism
- X-XSS-Protection: 1; mode=block

HTTP status return code 1xx (temporary response)
----------------------------------------
A status code that represents a temporary response and requires the requester to continue the operation.

=====     ========    ======================================================================
Code Code Description
=====     ========    ======================================================================
100 Continue The server returns this code to indicate that the first part of the request has been received and is waiting for the rest.
101 Switching protocol The requester has asked the server to switch the protocol, the server has confirmed and is ready to switch.
=====     ========    ======================================================================

HTTP status return code 2xx (success)
----------------------------------------
The status code indicating that the request was successfully processed.

=====     ==========    ======================================================================
Code Code Description
=====     ==========    ======================================================================
200 Success The server has successfully processed the request. Usually, this means that the server provides the requested webpage
201 Created The request was successful and the server created a new resource
202 Accepted The server has accepted the request, but has not been processed yet
203 Unauthorized information The server has successfully processed the request, but the returned information may be from another source
204 No content The server successfully processed the request but did not return any content
205 Reset content m server successfully processed the request but did not return any content
206 Some content The server successfully processed some GET requests
=====     ==========    ======================================================================

HTTP status return code 3xx (redirect)
----------------------------------------
It means that further operations are needed to complete the request. Typically, these status codes are used to redirect.

=====     ============    ======================================================================
Code Code Description
=====     ============    ======================================================================
More than 300 Choices The server can perform multiple operations for requests. The server can select an action based on the requester (user agent), or provide a list of actions for the requester to select.
301 Permanent Move The requested web page has been moved to the new location permanently. When the server returns this response (response to a GET or HEAD request), the requestor is automatically transferred to the new location.
302 Temporary Move The server currently responds to requests from web pages in different locations, but the requester should continue to use the original location to make future requests.
303 View Other Locations The server returns this code when the requester should use a separate GET request for different locations to retrieve the response.
304 Not modified Since the last request, the requested web page has not been modified. When the server returns this response, the content of the web page will not be returned.
305 Using a Proxy Requesters can only use the proxy to access the requested web page. If the server returns this response, it also means that the requester should use a proxy.
307 Temporary redirection The server currently responds to requests from web pages in different locations, but the requester should continue to use the original location to make future requests.
=====     ============    ======================================================================

HTTP status return code 4xx (request error)
----------------------------------------
These status codes indicate that a request may have an error, hindering the server's processing.

=====     ==================    ======================================================================
Code Code Description
=====     ==================    ======================================================================
400 Error request The server does not understand the syntax of the request.
401 Unauthorized Request for authentication. The server may return this response for web pages that need to be logged in.
403 Forbidden The server rejects the request.
404 Not Found The server cannot find the requested web page.
405 Method Disable Disable the method specified in the request.
406 Not accepted A web page that cannot respond to the requested content feature.
407 Requires proxy authorization This status code is similar to 401 (unauthorized), but specifies that the requester should authorize the proxy.
408 Request timeout A timeout occurred while the server was waiting for the request.
409 Conflict A conflict occurred when the server completed the request. The server must include information about the conflict in the response.
410 Deleted If the requested resource has been permanently deleted, the server returns this response.
411 Valid length required The server does not accept requests that do not contain the valid content length header field.
412 Prerequisite not met The server does not meet one of the prerequisites set by the requester in the request.
413 The requesting entity is too large The server cannot process the request because the requesting entity is too large, exceeding the server's processing capacity.
414 The requested URI is too long The requested URI (usually the URL) is too long and the server cannot handle it.
415 Unsupported Media Types The requested format is not supported by the requested page.
416 The request scope does not meet the requirements If the page cannot provide the requested scope, the server returns this status code.
417 Expected value not met The server did not meet the requirements of the "Expected" request header field.
=====     ==================    ======================================================================

HTTP status return code 5xx (server error)
----------------------------------------
These status codes indicate an internal error occurred on the server when trying to process the request. These errors may be errors in the server itself, not request errors.

=====     ==================    ======================================================================
Code Code Description
=====     ==================    ======================================================================
500 Internal Server Error The server encountered an error and could not complete the request.
501 Not yet implemented The server does not have the function to complete the request. For example, this code may be returned when the server fails to recognize the request method.
502 Error Gateway The server, as a gateway or proxy, received an invalid response from the upstream server.
503 Service Unavailable The server is currently unavailable (due to overload or downtime maintenance). Usually, this is just a temporary state.
504 Gateway timeout The server acts as a gateway or proxy, but does not receive the request from the upstream server in time.
505 HTTP version not supported The server does not support the HTTP protocol version used in the request.
=====     ==================    ======================================================================
