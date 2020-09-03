## Monitoring HTTP Headers 1

**1. Observe and explain each of the values monitored (use view source to see the plain messages)**  

I netværksfanen kan vi se én fil - i mit tilfælde *"Week2Day1-EX-1/"*.
I fanen kan vi se statuskode 200 (Betyder alt OK) samt om filen.

I fanen *"Sources"* kan vi se en folder-struktur med de(n) samme fil(er).

**2. Monitoring HTTP Headers 2**  

Efter at have tilføjet .css og et billede til websiden kan vi under fanen netværk undersøge headers for hver fil.
Under "General" på hver fil kan vi se informationer som request URL, request method (GET) og statuskode (200).
Desuden kan vi se response headers og request headers.  
Alle disse siger noget om hvordan klienten og servern kommunikerer.

**3. Monitoring HTTP Headers 3  (Response-codes 3xx)**  
Åbner vi vores side `localhost:8080/Week2Day1-EX-1` kan vi tilgå vores "index" side.
Skriver vi `localhost:8080/Week2Day1-EX-1/redirect` kan vi se 2 filer i netværksfanen.

- r.html: Siden vi oprettede
- redirect: Vi kan se i headeren at der er tale om en 302 - en re-direct.
I response headeren kan vi desuden se `Location: r.html`.  
Serveren re-directer altså requests til `localhost:8080/Week2Day1-EX-1/redirect` til `localhost:8080/Week2Day1-EX-1/r.html`

**3a. Redirecting to HTTPs instead of HTTP**  
Vi kan se, at den første request bliver håndteret med status 301 - en re-direct.
I response header kan vi se https under location.

Den næste request på listen er med status 200 som er https versionen af siden vi ender på.


**4a. Status codes (5xx)**  
Serveren genererer en 500 fejlkode med følgende stacktrace fra TomCat  

```java 
java.lang.ArithmeticException: / by zero
	Ups.processRequest(Ups.java:32)
	Ups.doGet(Ups.java:59)
	javax.servlet.http.HttpServlet.service(HttpServlet.java:626)
	javax.servlet.http.HttpServlet.service(HttpServlet.java:733)
	org.apache.tomcat.websocket.server.WsFilter.doFilter(WsFilter.java:53)
```
  

**4b. Status codes (4xx)**  
Serveren genererer en 404 fejlkode med følgende besked:

``The origin server did not find a current representation for the target resource or is not willing to disclose that one exists.``

**4c. Status codes - Ranges**  

- 2xx = Success
- 3xx = Redirection
- 4xx = Client errors
- 5xx = Server errors

*Easter egg: HTTP client error response [koden 418](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/418) oversættes til "418 I'm a teapot"*

**5. Get HTTP Request Headers on the server**  
Solved with some Java like this:

```java 
Enumeration<String> headerNames = request.getHeaderNames();
    while (headerNames.hasMoreElements()) {
        String headerName = headerNames.nextElement();
        System.out.println("Header Name - " + headerName + ", Value - " + request.getHeader(headerName));
```

**6. Get/Post-parameters**  
Ved at submitte en form som bruger GET kan form parametrene ses i URL. I dette tilfælde som `localhost:8080/WeekDay1-EX-1/getpost.html?fname=&lname=&hidden=12345678#`

Ændres formens metode til "POST" vil de indtastede data fremgå af "Form Data" som kan ses i "Network" i developer tools.
 
**7. Sessions (Session Cookies)**  

Den nuværende "State" opretholdes via. en session cookie som set på nedenstående billede:

<img src="https://github.com/MivleDK/3semFlow1Week2/blob/master/Day2/EX7.png">

Slettes denne session-cookie vil formularen dukke op igen, og der skal tastes et navn igen.

**8.  Persistent Cookies**  
I nedenstående billede ses både cookie oplysninger fra EX7("JSESSIONID") og EX8 ("username").  

Vi kan se, at sessionscookie udløber samtidig med sessionen.

<img src="https://github.com/MivleDK/3semFlow1Week2/blob/master/Day2/EX8.png">

For en persistent cookie bestemmer serveren (Rettere programmet på serveren) en cookies udløbstid - I dette tilfælde fremgår det af billedet.