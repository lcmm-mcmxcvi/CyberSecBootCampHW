## Unit

#### HTTP Requests and Responses

1. What type of architecture does the HTTP request and response process occur in?

    -  HTTP uses the `client-server architecture` in which a client will request certain resources from a server to which the server sends a response to.

2.  What parts make up an `HTTP request`?

    -  The parts of an `HTTP request` are: the `request line`, the `request headers`, and an optional `request body`.

3. What is the optional part of an HTTP request?

    -  The `request body`.

4. What three parts make up an HTTP response?

    -  The parts of an `HTTP response` are: the `status line`, the `response headers`, and the `response body`.

5. Which number "class" of status codes represent errors?

    -  `400` status codes represent errors.

6. What are the two most common request methods a security professional will come across?

    -  `GET` and `POST` requests.

7. Which type of HTTP request method is used for sending data?

    -  `POST` requests.

8. Which part of an `HTTP request` contains the data being sent to the server?

    -  The `request body`.

9. In which part of an HTTP response would the browser receive the web code to generate and style a web page?

    - The `response body`.

#### Using cURL

10. What are the advantages of using curl over the browser?

    - It allows you to easily see the response status lines, is repeatable, can be automated, and can be edited on the fly.

11. Which curl option is used to change the request method?

    - The curl option `-X` followed by a request method, such as `POST`, allows one to change the request method.

12. Which curl option is used to set request headers?

    - The curl option `-H` allows one to add a header to a request. For example: `curl example.com -H "Cookie: SessionID=Bob"`.

13. Which curl option is used to view the response header?

    - The curl option `-I` allows one to view the response header by itself.

14. Which request method might an attacker use to scope out usable HTTP requests that an HTTP server will accept?

    - An attacker is likely to use the `OPTIONS` request method for scoping out usable request methods.

### Sessions and Cookies

15. Which response header sends a cookie to the client?

    -  The `set-cookie` response header sends a cookie to the client. Note the following example similar to the `Bob example` from the lecture.

    ```HTTP
    HTTP/1.1 200 OK
    Content-type: text/html
    Set-Cookie: cart=Bob
    ```

16. Which request header sets a cookie in the client?

    - The `cookie` request header sets a cookie in the client. Note the following example similar to the `Bob example` from the lecture.

    ```HTTP
    GET /cart HTTP/1.1
    Host: www.example.org
    Cookie: cart=Bob
    ```

#### Example HTTP Requests and Responses

#### HTTP Request Example

```HTTP
POST /login.php HTTP/1.1
Host: example.com
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Type: application/x-www-form-urlencoded
Content-Length: 34
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Linux; Android 6.0; Nexus 5 Build/MRA58N) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.132 Mobile Safari/537.36

username=Barbara&password=password
```

17. What was the request method?

    - The request method in this example was `POST`.

18. Was the request encrypted or unencrypted?

    - The request was not encrypted, even though the browser is requesting an upgraded to HTTP/2 connection.

19. Does the request have a user session associated to it?

    - The request does not have a `Cookie` header set so there is no indication that a user session is associated with this request.

20. What kind of data is being sent from from this request body.

    -  It should be pretty clear from the request body that this request is an attempt to authenticate into the site's `login.php` page.

#### HTTP Response Example

```HTTP
HTTP/1.1 200 OK
Date: Mon, 16 Mar 2020 17:05:43 GMT
Last-Modified: Sat, 01 Feb 2020 00:00:00 GMT
Content-Encoding: gzip
Expires: Fri, 01 May 2020 00:00:00 GMT
Server: Apache
Set-Cookie: SessionID=5
Content-Type: text/html; charset=UTF-8
Strict-Transport-Security: max-age=31536000; includeSubDomains
X-Content-Type: NoSniff
X-Frame-Options: DENY
X-XSS-Protection: 1; mode=block

[page content]
```

21. What was the response status code?

    - The status code returned with a `200 OK`.

22. Was the response encrypted or unencrypted?

    -  The response was not encrypted that can be evidence with the status line `HTTP/1.1`.

23. Does this response have a user session associated to it?

    - This user does have a session associated with them as seen by the `set-cookie` header.

24.  What kind of content is likely to be in the [page content] response body?

    - Judging by the `content-type: text/html` header, the response body contains the site's web code.

25. If your class covered security headers, what security request headers have been included?

    - There are actually a lot of security headers in this example, but the one covered in class would have been `Strict-Transport-Security` which tells the client that it should only be accessed over HTTPS and not HTTP.

#### Monoliths and Microservices

26. What are the individual components of microservices called?

    -  When a monolith's components are separated by functions, they are called `services`.

27. What is a service that writes to a database and communicates to other services?

    -  An `Application Programming Interface` or `API` is a service that allows people to interact directly with back-end-like services.

28. What type of underlying technology allows for `microservices` to become scalable and have redundancy?

    -  Containers allow microservices to be both scalable and redundant.

#### Container Vulnerability Filtering

29. Do `microservices` share the same kind of vulnerabilities as regular operating systems?

    -  Yes, microservices have the same vulnerabilities as regular operating systems.

30. Would an organization be more concerned with `Low` severity vulnerabilities as much as `Critical`?

    -  Generally no, we ignored low severity vulnerabilities for our activity.

31. Would the bash tool `jq` be useful in finding certain kinds of vulnerabilities within a vulnerability report?

    -  As we saw in our vulnerability filtering activity, it definitely is. It can also be used to create new JSON reports for log aggregators.

#### Deploying and Testing a Container Set

32. What is a tool that can be used to deploy multiple containers at once?

    -  Docker-Compose can be used to deploy multiple containers as individual "services".

33. What kind of file format was required for us to deploy a container set?

    -  A `YAML` file, specifically in our case, `docker-compose.yml`.

#### Container Runtime Intrusion Detection Systems

34. What is a tool to that actively detects for intrusion behavior within containers?

    -  The container intrusion detection system we looked at is called `Falco`.

35. What high-value system file might an intruder view that would trigger a `sensitive file opening` alert?

    -  `/etc/shadow` is the typically the most sensitive file within a Linux system that intruder may access the contents of.

36. What kind of intruder action might trigger an alert from a container IDS that says `shell configuration file has been modified`?

    -  The creation of users triggered this alert.

---

© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.
