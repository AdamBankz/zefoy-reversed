
CAPTCHA Solving
---
<img width="273" height="91" alt="image" src="https://github.com/user-attachments/assets/e9ec5055-b469-49a5-a2f6-171a632b78fc" /><br>
When I solved the following CAPTCHA and submitted the solution, a POST request was made to `zefoy.com`, once the backend confirmed the solution was correct, the request got a 302 Response and my page refreshed, unlocking the dashboard. The CAPTCHA completion links to my PHPSESSID.
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
1. The value for the first key is the plain text of solution submitted. Simple and easy.
2. The value for the second key is an encoded string.
3. The value for the third key is a ciphered JSON
   - This includes `ct`, `iv` and `s`, which is Ciphertext, Initialisation Vector and the Salt.
   - In order to decode this, you need the logic used to encode it.
  
Seeing this, I looked into Zefoy's Javascript. > https://zefoy.com/assets/53fbc84b11a13a7942a850361e5d7b49.js?v=1754384581<br>
As they used [obfuscator.io](obfuscator.io) to obfuscate their Javascript, it was incredibly easy to make it readable.<br>
