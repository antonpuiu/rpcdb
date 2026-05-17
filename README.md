# Proiect RPC Client/Server Application

[cite_start]**Autor:** Puiu Anton [cite: 1]  
[cite_start]**Grupa:** 343C3 [cite: 1]  
[cite_start]**Sistem de operare target:** Linux [cite: 1]  

---

## 📌 Descriere Generală
Proiectul implementează o arhitectură **Client/Server** bazată pe RPC (Remote Procedure Call) pentru execuția de comenzi de la distanță.

### 💾 Modelarea Datelor & Protocolul de Comunicație
* [cite_start]Pentru fiecare comandă executată de către client, s-a definit o pereche dedicată de structuri de date: `request` și `response`[cite: 2].
* [cite_start]În cazurile în care structura de date definită pentru o comandă este similară sau identică pentru o altă comandă, se păstrează o singură structură de date reutilizabilă pentru mai multe comenzi[cite: 3]. [cite_start]De exemplu, pentru structura `request` a comenzilor `DELETE`, `READ` și `GET_STAT`, se utilizează aceeași structură de date[cite: 4].
* [cite_start]Pentru a reprezenta structurile `request` și `response`, se utilizează uniuni, întrucât trebuie înglobate structurile de date pentru fiecare grup de comenzi[cite: 9].
* [cite_start]Comanda executată de către client este definită prin tipul de date enumerare `command_type`[cite: 5].

### 🔌 Interfața RPC
[cite_start]Interfața expune o singură funcție care poate fi apelată de către client, mai exact `rpc_call`[cite: 6].
* [cite_start]Comanda executată de către client este specificată prin intermediul parametrului `type` de tipul `command_type`[cite: 7].
* [cite_start]Serverul întoarce tipul comenzii executate de către client, sau valoarea `BAD_CMD` în caz de eroare[cite: 8].

---

## 💻 Arhitectură Componente

### 1. Clientul
[cite_start]Pentru a executa o comandă, pe partea de client se parcurg următorii pași[cite: 10]:
1. [cite_start]Se citește din fișier sau de la tastatură o linie[cite: 10].
2. [cite_start]Se interpretează linia citită[cite: 10].
3. [cite_start]Se construiește cererea[cite: 10].
4. [cite_start]Se execută comanda[cite: 10].
5. [cite_start]Se interpretează răspunsul[cite: 10].

[cite_start]Pentru construirea cererii și interpretarea răspunsului sunt definite două clase abstracte, care reprezintă clasele de bază pentru fiecare tip de cerere, respectiv răspuns[cite: 10]. [cite_start]Ierarhia de clase se poate observa din structura de directoare prezentă, aceasta fiind creată cu scopul reutilizării optime a codului[cite: 11].

### 2. Serverul
[cite_start]Pentru a executa o comandă, pe partea de server se parcurg următorii pași[cite: 12]:
1. [cite_start]Se interpretează cererea[cite: 12].
2. [cite_start]Se execută cererea[cite: 12].
3. [cite_start]Se construiește răspunsul[cite: 12].

[cite_start]Cei trei pași menționați anterior se realizează în cadrul unui singur obiect, mai exact o instanță a clasei `command`, întrucât separația realizată în cazul clientului nu este necesară[cite: 12].

---

## 🛠️ Compilare și Rulare

### Cerințe preliminare
* [cite_start]Compilarea temei necesită instalarea utilitarului **CMake**[cite: 13].
* [cite_start]Este necesară prezența bibliotecii **rpcbind** în sistem[cite: 13].

### Instrucțiuni de utilizare
* [cite_start]**Compilarea proiectului:** Se realizează prin lansarea în execuție a scriptului dedicat `compile.sh`[cite: 13].
* [cite_start]**Rularea testelor:** Pentru rularea suitei de teste este pus la dispoziție scriptul `run_tests.sh`[cite: 14].
