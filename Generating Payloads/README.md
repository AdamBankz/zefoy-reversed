Generating Payloads 
---
The first interaction you'll face on the website is the CAPTCHA. When you submit a correct solution, it sends a POST Request to `zefoy.com`. If the CAPTCHA is checked and correct, it refreshes the page and loads the dashboard.
The headers sent in the request are `PHPSESSID` and `ltj`, which have been analysed [here](https://github.com/AdamBankz/zefoy-reversed/blob/main/Signing%20Requests/README.md).


CAPTCHA Solving
---
<img width="273" height="91" alt="image" src="https://github.com/user-attachments/assets/e9ec5055-b469-49a5-a2f6-171a632b78fc" /><br>
When I solved the following CAPTCHA and submitted the solution, a POST request was made to `zefoy.com`, once the backend confirmed the solution was correct, the request got a 302 Response and my page refreshed, unlocking the dashboard. The CAPTCHA completion links to my PHPSESSID, enabling persistence. Ensuring that I do not have to redo it when refreshing the page.
<br><br>
The payload that was sent during submission is below. It looks overwhelming and complex, in reality it's just low-level encoding.
<img width="2051" height="670" alt="image" src="https://github.com/user-attachments/assets/bbe5bad9-7e5e-46ce-992c-59b4efeba934" />
The Form Name keys in the POST Request are present on your first GET request to `zefoy.com`. They are generated dynamically and are verified by the backend. They can be extracted like this:


```py
# Extract the first key in the payload  (9467f3d825ca70a18c1e)
text_input = soup.select_one("input#captchatoken")
text_input_name = text_input["name"]

# Extract the second key in the payload  (9c1ce27f08b16479d2e17743062b28ed)
hidden_input = soup.select_one("input[type='hidden'][class='input']")
hidden_name = hidden_input["name"]

# The captcha_encoded key is static and it's name will not change
```
The value for the first key is the plain text of solution submitted. Simple and easy.
