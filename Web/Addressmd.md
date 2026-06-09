# Write-up: Address

<img width="830" height="173" alt="image" src="https://github.com/user-attachments/assets/00f2e93a-0279-4a44-8763-d68d06be1f2d" />


![Author](https://img.shields.io/badge/Author-Lucian_Ioan_Nitescu-red?style=for-the-badge)

![Category](https://img.shields.io/badge/Category-Web%20Exploitation-orange?style=for-the-badge&logo=kalilinux)

![Difficulty](https://img.shields.io/badge/Difficulty-Easy-yellow?style=for-the-badge)

![Points](https://img.shields.io/badge/Points-10-success?style=for-the-badge)

![Status](https://img.shields.io/badge/Status-SOLVED-brightgreen?style=for-the-badge)          

## Odata cu accesarea paginii web, vom gasi un meme care vorbeste despre adrese

<img width="1801" height="937" alt="image" src="https://github.com/user-attachments/assets/aa8defb1-0008-4fb0-aed8-42bbfd67e79b" />


## In inspector putem gasi un comment cu pagina "/admin.php"

<img width="1465" height="726" alt="image" src="https://github.com/user-attachments/assets/12267e89-366f-4170-a27a-8e48c84ccb32" />


## Dupa accesarea acesteia putem vedea ca ne cere sa fim localhost :

<img width="1371" height="781" alt="image" src="https://github.com/user-attachments/assets/0ffc7624-5b31-4cd7-a8fa-4e336f43b281" />

## Asa ca trimitem un request de tip POST cu X-Forwarded-For: 127.0.0.1 pentru a obtine flag-ul

```python
curl -X POST http://34.159.220.97:32232/admin.php -H "X-Forwarded-For: 127.0.0.1"
```


<img width="679" height="61" alt="image" src="https://github.com/user-attachments/assets/6edbc356-6e55-48f0-bda6-3b2f749760c0" />

