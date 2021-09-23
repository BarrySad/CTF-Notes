# Cody's First Blog
## First thoughts
- very basic looking blog website
- the comment box has definitely caught my attention right away, maybe a form of XSS or SQLI could work
- the submit button also looks promising
- lastly, the "First post! I built this blog engine around one basic concept: PHP doesn't need a template language because it _is_ a template language. This server can't talk to the outside world and nobody but me can upload files, so there's no risk in just using include()." blog update seems like a clue

## Flag0
- For this flag my first thought was to just open up Burp Suite and find out what the site is running 
- Turns out it is running PHP 5.5.9 and Nginx 1.14.0, which means the website uses PHP to communicate with the server
- Surprisingly enough PHP 5.5.9 has a **TON** of security problems, making RCE very easy to pull off
- First I am going to try a basic PHP echo script and see what happens `<?php echo "HELLO"; ?>`
- And just like that the flag is populated right onto the content submit page

## Flag1
- One of the first things I look at when looking for website vulnerabilities is the source code, and I very quickly noticed a bit of code that shouldn't have been there `<!--<a href="?page=admin.auth.inc">Admin login</a>-->`
- Entering that `?page=admin.auth.inc` into the URL loads an Admin Login page, and one thing that's always exciting is finding an unlisted custom login page
- From what I can tell this login page is pretty protected, it replies with "Incorrect username or password" which makes brute forcing with something like hydra out of the question 
- Even using some common SQL injection methods like entering `admin' OR 1'` into the Username field did nothin
- The answer was actually painfully simple, I just had to change the URL to `page=admin.inc` instead of `page=admin.auth.inc`. Evidently in PHP 5.5.9 this just skips admin authentication