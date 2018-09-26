# Attacking Webviews

Webiviews offer many benefits to mobile application developers including the ability to reuse existing code between apps, patch applications quickly, and use comfortable technoligies. 

Webviews also present security challenges in both iOS and Android. Traditional web application vulnerabilities such as Cross-Site Scripting and other forms of injection may exist in WebViews if not configured properly.

## Task 1: Open the DVIA WebView Lab

In the simulator running on your local machine, open the DVIA app and navigate to `Webview Issues` and click `Start Challenge`

You will see that anything typed in the top text box will be displayed below in HTML.

## Task 2: Inject Javascript
Since WKWEbViews will not display alert boxes our old school XSS payload of `<script>alert('xss')</script> will not work`

The four challenges on this page also may not work reliably in  the simulator.

To test if we have a vulnerable WebView, enter the following:
```
<h1>testing</h1>
```
As you can see, we are able to inject HTML as the text is an `<H1>` heading.

## Challenge:
What else can you enter in the input box to prove the WebView is vulnerable? Try out some payloads on your own!

Hint: Going back to the 90's...