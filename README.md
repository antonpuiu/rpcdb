# Proiect RPC Client/Server Application

**Autor:** Puiu Anton

**Grupa:** 343C3

**Sistem de operare target:** Linux

---

## 📌 Descriere Generală
Proiectul implementează o arhitectură **Client/Server** bazată pe RPC (Remote Procedure Call) pentru execuția de comenzi de la distanță.

### 💾 Modelarea Datelor & Protocolul de Comunicație
* Pentru fiecare comandă executată de către client, s-a definit o pereche dedicată de structuri de date: `request` și `response`
* În cazurile în care structura de date definită pentru o comandă este similară sau identică pentru o altă comandă, se păstrează o singură structură de date reutilizabilă pentru mai multe comenzi. De exemplu, pentru structura `request` a comenzilor `DELETE`, `READ` și `GET_STAT`, se utilizează aceeași structură de date.
* Pentru a reprezenta structurile `request` și `response`, se utilizează uniuni, întrucât trebuie înglobate structurile de date pentru fiecare grup de comenzi.
* Comanda executată de către client este definită prin tipul de date enumerare `command_type`.

### 🔌 Interfața RPC
Interfața expune o singură funcție care poate fi apelată de către client, mai exact `rpc_call`.
* Comanda executată de către client este specificată prin intermediul parametrului `type` de tipul `command_type`.
* Serverul întoarce tipul comenzii executate de către client, sau valoarea `BAD_CMD` în caz de eroare.

---

## 💻 Arhitectură Componente

### 1. Clientul
Pentru a executa o comandă, pe partea de client se parcurg următorii pași:
1. Se citește din fișier sau de la tastatură o linie.
2. Se interpretează linia citită.
3. Se construiește cererea.
4. Se execută comanda.
5. Se interpretează răspunsul.

Pentru construirea cererii și interpretarea răspunsului sunt definite două clase abstracte, care reprezintă clasele de bază pentru fiecare tip de cerere, respectiv răspuns. Ierarhia de clase se poate observa din structura de directoare prezentă, aceasta fiind creată cu scopul reutilizării optime a codului.

### 2. Serverul
Pentru a executa o comandă, pe partea de server se parcurg următorii pași:
1. Se interpretează cererea.
2. Se execută cererea.
3. Se construiește răspunsul.

Cei trei pași menționați anterior se realizează în cadrul unui singur obiect, mai exact o instanță a clasei `command`, întrucât separația realizată în cazul clientului nu este necesară.

---

## 🛠️ Compilare și Rulare

### Cerințe preliminare
* Compilarea temei necesită instalarea utilitarului **CMake**.
* Este necesară prezența bibliotecii **rpcbind** în sistem.

### Instrucțiuni de utilizare
* **Compilarea proiectului:** Se realizează prin lansarea în execuție a scriptului dedicat `compile.sh`.
* **Rularea testelor:** Pentru rularea suitei de teste este pus la dispoziție scriptul `run_tests.sh`.
