# Lab 11 – Docker - Projekt z PAwChO 2024/2025

---

## Autor

EMIL ŁOŚ 99609

---

## Co zostało zrobione (krok po kroku)

### Stworzenie odpowednich katalogów

- Stworzenie sieci.

lab11_docker docker network create --driver bridge lab11net
wynik:
9bdd0c7c2e56774668f90af01a67bc15dec9e9736bb64bfd211fc042b19e7e33

---
- Tworzenie kontenerów

# web1

lab11_docker docker run -d --name web1 --network lab11net -p 8081:80 --mount type=bind,source=$(pwd)/web1,target=/usr/share/nginx/html,readonly --mount type=bind,source=$(pwd)/lab11/web1/logs,target=/var/log/nginx nginx:latest
wynik:
c558a1f3e6db8941603ca5c660266ced8a790814d5016133f510b5c2f988a7f4

# web2

lab11_docker docker run -d --name web2 --network lab11net  -p 8082:80 --mount type=bind,source=$(pwd)/web2,target=/usr/share/nginx/html,readonly --mount type=bind,source=$(pwd)/lab11/web2/logs,target=/var/log/nginx nginx:latest 
wynik:
146c0fe0bbcd298b94f7d39b8cf8ca8ef03f5e3cc1f4fd36dfc8ebab66b0b442

# web3

lab11_docker docker run -d --name web3 --network lab11net -p 8083:80 --mount type=bind,source=$(pwd)/web3,target=/usr/share/nginx/html,readonly --mount type=bind,source=$(pwd)/lab11/web3/logs,target=/var/log/nginx nginx:latest 
wynik:
97a94b6e888f2e3e289f9cba96a76049b217f8a74a9635d09b217dcfa18f56ca

---

### SPRAWDZENIE STRON

lab11_docker curl http://localhost:8081

<html><body><h1>Laboratorium 11 - Emil Łoś - web1</h1></body></html>%    


➜  lab11_docker curl http://localhost:8083

<html><body><h1>Laboratorium 11 - Emil Łoś - web3</h1></body></html>%                                        

➜  lab11_docker curl http://localhost:8082

<html><body><h1>Laboratorium 11 - Emil Łoś - web2</h1></body></html>%    

### PRZYKLADOWE LOGI Z WEB1

 lab11_docker cat lab11/web1/logs/access.log

192.168.65.1 - - [25/May/2025:21:49:43 +0000] "GET / HTTP/1.1" 200 70 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/18.5 Safari/605.1.15" "-"
192.168.65.1 - - [25/May/2025:21:49:43 +0000] "GET /favicon.ico HTTP/1.1" 404 153 "http://localhost:8081/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/18.5 Safari/605.1.15" "-"
192.168.65.1 - - [25/May/2025:21:49:43 +0000] "GET /apple-touch-icon-precomposed.png HTTP/1.1" 404 153 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Safari" "-"
192.168.65.1 - - [25/May/2025:21:49:43 +0000] "GET /apple-touch-icon.png HTTP/1.1" 404 153 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Safari" "-"
192.168.65.1 - - [25/May/2025:21:51:29 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/18.5 Safari/605.1.15" "-"
192.168.65.1 - - [25/May/2025:21:53:12 +0000] "GET / HTTP/1.1" 200 70 "-" "curl/8.7.1" "-"
