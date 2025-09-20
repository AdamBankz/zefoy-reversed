Generating Payloads 
---
The first interaction you'll face on the website is the CAPTCHA. When you submit a correct solution, it sends a POST Request to `zefoy.com`. If the CAPTCHA is checked and correct, it refreshes the page and loads the dashboard.
The headers sent in the request are `PHPSESSID` and `ltj`, which have been analysed [here](https://github.com/AdamBankz/zefoy-reversed/blob/main/Signing%20Requests/README.md).



