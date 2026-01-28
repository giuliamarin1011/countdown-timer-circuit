# countdown-timer-circuit

                                   

	Baza proiect

	8 ore aprins
	16 ore stins
	Un LED trebuie sa fie pe ON 8 ore ai pe OFF 16
	24 de stari- 0 – 23
	Nr maxim de biti 2^n-1 => cu 5 biti reprezint de la 0-31

0  = 00000
1  = 00001
2  = 00010
...
7  = 00111
8  = 01000
...
15 = 01111
16 = 10000
...
23 = 10111
	8 ore ON –orele 0-7
	16 ore OFF- orele 8-23
	Iesiri binare: Q0,Q1,Q2,Q3,Q4

1.INTRĂRI - sunt semnale din exterior care controlează circuitul.
          -CLK (Clock – impuls pe oră)    -cea mai importantă intrare.
                                                               -la fiecare impuls, contorul crește cu 1.


2.IESIRI- sunt semnale produse de circuit.
-  Q4, Q3, Q2, Q1, Q0     -cei 5 biți ai contorului
                                           -reprezintă numărul de la 0 la 23 (ora curenta)

         -LED   -ieșirea finală care controlează LED-ul.


 3. CONDIȚII DE CONTROL -sunt semnale interne sau reguli care controlează funcționarea circuitului.
- Regula incrementării   -contorul trebuie să crească cu 1 la fiecare impuls de clock.
-Resetarea la 24 (modulo-24)  -contorul NU are voie să continue până la 31.
                                                     -trebuie să se reseteze la 0 când ajunge la 24.
Starea 24 = 11000
Funcția de detecție:
Detect24=Q4⋅Q3⋅¬Q2⋅¬Q1⋅¬Q0 
detect24 = 1 =>Contorul sare la 0
-LED control:  LED = 1 pentru Q < 8 (adica Q4=0 si Q3=0)

 4. MODUL DE REPREZENTARE A DATELOR 
    Ora curentă este reprezentată intern în format binar, pe 5 biți, folosind ieșirile contorului modulo-24 (Q4, Q3, Q2, Q1, Q0). Astfel se pot reprezenta valorile de la 0 la 23 (în binar: 00000 – 10111).  Pentru afișarea valorilor într-o formă ușor de înțeles, se folosește o memorie ROM conectată la
ieșirile contorului. Biții Q4 Q3 Q2 Q1 Q0 sunt folosiți ca adresă în ROM, iar la ieșirea ROM se obține
codul ce este aplicat unui afișor de tip HEX. În acest fel are loc conversia din reprezentarea binară internă în format numeric afișabil (zecimal/hexazecimal) în Logisim.



	Tabelul de adevar - cu ora, starea curenta, starea urmatoare si iesirea LED
	LED = 1 pentru orele 0–7 (primele 8 stări)
	LED = 0 pentru orele 8–23
Ora (zecimal)	Stare curentă Q4 Q3 Q2 Q1 Q0	Stare următoare Q4' Q3' Q2' Q1' Q0'	LED
0	00000	00001	1
1	00001	00010	1
2	00010	00011	1
3	00011	00100	1
4	00100	00101	1
5	00101	00110	1
6	00110	00111	1
7	00111	01000	1
8	01000	01001	0
9	01001	01010	0
10	01010	01011	0
11	01011	01100	0
12	01100	01101	0
13	01101	01110	0
14	01110	01111	0
15	01111	10000	0
16	10000	10001	0
17	10001	10010	0
18	10010	10011	0
19	10011	10100	0
20	10100	10101	0
21	10101	10110	0
22	10110	10111	0
23	10111	00000	0

Tabelul minimizat pentru Detect24(funcție combinațională care devine 1 doar când contorul are valoarea 24).

Detect24=Q4⋅Q3⋅¬Q2⋅¬Q1⋅¬Q0

Q4	Q3	Q2	Q1	Q0	Detect24
1	1	0	0	0	1
altfel	altfel	altfel	altfel	altfel	0


	Functia pentru LED
 -Q4 – bitul cel mai semnificativ
-  Q3
- Q2
- Q1
- Q0 – bitul cel mai puțin semnificativ
Voi folosi notatia  ¬¬¬¬¬¬ pentru NOT ( ¬O4=NOT Q4 )
LED = 1 pentru mintermele 0,1,2,3,4,5,6,7
                        LED(Q4,Q3,Q2,Q1,Q0)=∑m(0,1,2,3,4,5,6,7) 
Explicit: 
m₀ (00000)
m0=¬Q4 ¬Q3 ¬Q2 ¬Q1 ¬ Q0
m₁ (00001)
m1=¬Q4 ¬Q3 ¬Q2 ¬Q1 Q0 
m₂ (00010)
m2=¬Q4 ¬Q3 ¬Q2 Q1 ¬Q0  
m₃ (00011)
m3=¬Q4 ¬Q3 ¬Q2 Q1 Q0 
m₄ (00100)
m4=¬Q4 ¬Q3 Q2 ¬Q1 ¬Q0   
m₅ (00101)
m5=¬Q4 ¬Q3 Q2 ¬Q1 Q0   
m₆ (00110)
m6=¬Q4 ¬Q3 Q2 Q1 ¬Q0 
m₇ (00111)
m7=¬Q4 ¬Q3 Q2 Q1 Q0   

Functia LED:
 LED=m0+m1+m2+m3+m4+m5+m6+m7
 adica:
LED=¬Q4¬Q3¬Q2¬Q1¬Q0+¬Q4¬Q3¬Q2¬Q1Q0+¬Q4¬Q3¬Q2Q1¬Q0+¬Q4¬Q3¬Q2Q1Q0+¬Q4¬Q3Q2¬Q1¬Q0+¬Q4¬Q3Q2¬Q1Q0+¬Q4¬Q3Q2Q1¬Q0+¬Q4¬Q3Q2Q1Q0
 Cum toti termenii contin ¬Q4 ¬Q3, dam factor comun, obtinand: 
LED=¬Q4¬Q3(¬Q2¬Q1¬Q0+¬Q2¬Q1Q0+¬Q2Q1¬Q0+¬Q2Q1Q0+Q2¬Q1¬Q0+Q2¬Q1Q0+Q2Q1¬Q0+Q2Q1Q0)
Cum paranteza contine toate combinatiile posibile pentru Q1Q2Q0 – unul din termenii din paranteza va fi 1 => paranteza este egala cu 1.
Asadar, functia se va reduce la
 LED= ¬Q4·¬Q3.

     Pentru circuitele secvențiale (numărător modulo-24) au fost definite toate combinațiile posibile ale stării curente (0–23), împreună cu starea următoare și ieșirea LED.
    Pentru circuitele combinaționale (LED, Detect24) au fost definite toate combinațiile posibile ale intrărilor Q4…Q0. LED devine 1 pentru combinațiile 00000–00111 și 0 pentru restul, iar Detect24 devine 1 doar pentru combinația 11000 și 0 pentru toate celelalte.

    Pe baza tabelului de adevăr și a tabelului de stări al numărătorului modulo-24 au fost obținute funcțiile logice ale circuitelor combinaționale.
Ieșirea LED depinde de biții Q4 și Q3 ai contorului, rezultând funcția minimizată:
                                                                       LED=¬Q4⋅¬Q3   
     Semnalul de resetare (Detect24) devine activ doar când contorul atinge valoarea binară 11000 (24 zecimal), rezultând funcția:
                                                                     Detect24=Q4⋅Q3⋅¬Q2⋅¬Q1⋅¬Q0


	Minimizarea funcțiilor cu diagramele Veitch-Karnaugh 
       Pentru minimizarea funcțiilor logice s-au utilizat diagramele Veitch–Karnaugh.
În cazul funcției LED, în diagrama Karnaugh se observă că ieșirea este 1 pentru toate combinațiile în care Q4 = 0 și Q3 = 0, indiferent de valorile lui Q2, Q1, Q0. Gruparea acestor termeni conduce la expresia minimizată:
                                                      LED=¬Q4⋅¬Q3 
      Pentru funcția Detect24, diagrama Karnaugh conține un singur termen de valoare 1 (corespunzător combinației 11000₂), care nu poate fi grupat cu alți termeni, astfel încât expresia rămâne:
                               Detect24=Q4⋅Q3⋅¬Q2⋅¬Q1⋅¬Q0

	Componentele pentru circuite
      Pentru implementarea numărătorului modulo-24 s-a utilizat un contor binar de 5 biți (componenta Counter din Logisim), configurat ca numărător sincron crescător. Intrarea sa de clock controlează incrementarea stării, iar intrarea de reset este activată prin semnalul Detect24.
   Pentru generarea semnalului LED s-au utilizat două porți NOT (pentru negarea biților Q4 și Q3) și o poartă AND cu două intrări, corespunzătoare expresiei minimizate LED=¬Q4⋅¬Q3
      Pentru detectarea stării 24 (11000₂) s-au folosit trei porți NOT pentru negarea biților Q2, Q1 și Q0, precum și porți AND pentru combinarea celor cinci variabile, conform expresiei Detect24=Q4⋅Q3⋅¬Q2⋅¬Q1⋅¬Q0   
Semnalul Detect24 este conectat la intrarea de reset a numărătorului pentru realizarea funcționării modulo-24.
     Pentru afișarea valorii contorului s-a utilizat o memorie ROM conectată la ieșirile contorului. Ieșirea ROM este trimisă către un afișor HEX, realizând conversia din reprezentare binară în zecimal/hexazecimal.
     
6) Prezentarea funcționării circuitului
     Circuitul realizat este un sistem de temporizare bazat pe un numărător modulo-24. Intrarea de clock generează un impuls periodic (o dată pe oră), iar contorul de 5 biți incrementează starea curentă la fiecare impuls. Astfel sunt reprezentate toate orele între 0 și 23 în format binar pe ieșirile Q4…Q0. Atunci când contorul ajunge în starea 24 (11000₂), circuitul combinațional Detect24 devine activ. Acest semnal este conectat la intrarea de reset a numărătorului și determină revenirea imediată în starea 0, realizând astfel funcționarea modulo-24.
    Ieșirea LED este controlată de o funcție combinațională derivată din tabelul de adevăr: LED = ¬Q4 · ¬Q3. Această expresie este implementată cu două porți NOT și o poartă AND. LED-ul este aprins (valoare logică 1) doar în primele 8 stări ale numărătorului, corespunzătoare intervalului 0–7, în care biții Q4 și Q3 sunt amândoi 0. Pentru valorile 8–23, cel puțin unul dintre biții Q4 sau Q3 devine 1, iar ieșirea LED se stinge. Rezultatul este un circuit de temporizare în care LED-ul este aprins timp de 8 ore și stins timp de 16 ore, apoi ciclul se repetă continuu.
Conversia și afișarea valorilor binare utilizând o memorie ROM și afișoare HEX
    Pentru afișarea valorii contorului într-o formă ușor de interpretat, am utilizat un modul de memorie ROM conectat la ieșirile numărătorului. Biții Q4…Q0 ai contorului reprezintă adresa ROM-ului, permițând accesarea celor 24 de valoari necesare (0–23). În memoria ROM a fost configurat un tabel corespunzător fiecărei adrese, astfel încât la ieșire sunt generate codurile adecvate pentru un afișor HEX (sau două afișoare, în cazul afișării zecimale). Ieșirea ROM este conectată la afișorul HEX, care afișează valoarea numerică a contorului în timp real. În acest mod se realizează conversia din reprezentarea binară internă în formă vizuală, permițând monitorizarea ușoară a stării curente a circuitului.




