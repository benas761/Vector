Vector

Paleidimo instrukcija:
- Naudojimui reikia vector.h failą perkelti į programos aplaką ir programoje prirašyti ```#include "vector.h"```
- Norint paleisti testą reikia:
   - Ant windows: sukurti projektą su codeblocks, įklijuoti norimo testo kodą į main.cpp, nukopijuoti vector.h į aplankalą ir paleisti.
   - Ant unix: perkelti vector.h į testų aplankalą ir per konsolę įvesti ```g++ -o main [testo pavadinimas].cpp vector.h``` ir ```./main```.

1. Vektorius veikia ne taip, kaip orginalus. 
  - 2/22 testai neišlaikyti (reserve() dėl šablono neveikimo su alokatoriumis, emplace_back dėl  nesuderinamumo su perkelimo kostruktoriaus kūrimu prie to pačio nesukuriant ir kopijavimo konstruktoriaus)
  - Neveikia su c++11 for ciklais kai vektorius atsiunčiamas kaip const.

Funkcijų aprašymai:
  - operator=: Jei vektoriai nelygūs, ištrina vektorių ir pagal konstruktorių sukuria atsiųsto vektoriaus kopiją. Jei lyginta naudojant std::move, tai dar ištrina atsiųstą vektorių.
  - assign: siunčiant vektorių daro tą pati kaip = operatorius. Siunčiant 2 (n, m) skaičius vektorių ištrina ir užpildo n vietų m reikšme. Siunčiant iteratorius, ištrina vektorių ir užpildo pagal iteratorių suformuoto sąrašo reikšmes. Siunčiant sąrašą vektorių priskiria sąrašo reikšmėms.
  - push_back: šaukiamas emplace_back(std::move).
  - pop_back: ištrina 1 vektoriaus elementą.
  - clear: ištrina visus elementus ir padaro vektoriaus dydį 0. Nekeičia vektoriaus talpos.
  - reserve: Jei neužtenka vietos, sukuria naują vektorių, jam priskiria senojo vektoriaus reikšmes, ištrina seną vektorių ir jį priskiria naujam.
  - resize: Jei vektoriaus dydis mažesnis už nusiųstą skaičių, iškviečia reserve() ir užpildo tuščias vietas 0. Jei vietos daugiau, sumažina vektorių iki atsiųsto dydžio ištrindama netelpančias reikšmes.
  - Shrink_to_fit: Panašu į rezerve su didesniais už talpą skaičiais, tačiau ši funkcija sumažina vektorių iki tokios talpos, kiek yra elementų.
  - erase: ištrina reikšmę norimoje pozicijoje arba intervale ir gražina tos pozicijos arba intervalo pradžios iteratorių.
  - insert: įterpia elementą į poziciją perkeldama visus elementus per vieną. Jei siunčiamas intervalas pagal iteratorius, visi elementai perkeliami per last-first vietų. Jei nepakanka vietos, išsaugomas atstumas tarp vektoriaus pradžios ir pozicijos, padidinamas vektorius ir iš naujo nustatomas pozicijos iteratorius.
  - emplace_back: nusiunčia reikšmę vektoriaus tipo konstruktoriui, kuris įveda reikšmę į vektoriaus pabaigą.
  - emplace: perkelia visus elementus nuo pozicijos per 1 ir per tipo konstruktorių iterpia reikšmę.
2. Analyzė įvykdyta su time_test.cpp:
    - Su 10000:
        - std::vector: 0.000596235s
        - Vector.h: 0.000713018s
    - Su 100000:
        - std::vector: 0.00297857s
        - Vector.h: 0.0014574s
    - Su 1000000:
        - std::vector: 0.015446s
        - Vector.h: 0.0183329s
    - Su 10000000:
        - std::vector: 0.138447s
        - Vector.h: 0.161238s
    - Su 100000000:
        - std::vector: 1.31019s
        - Vector.h: 1.50316s
    
Sistemos aprašymas:
- Intel(R) Core(TM) i5-8265U CPU @ 1.60GH
- 2 * 4GB DDR4 RAM
- SSD

3. Kadangi programa skaičiuoja 256 sekundes su 10^7, pamatuoti perrinkimų skaičių su 10^8 labai ilgai užtruktų. Skaičiuojant su 10^6 abu konteiniariai padarė 18 perrinkimų.
4. Vektorius tinkamai veikia su 3 užduotimi. Modifikuota užduotis yra aplanke "3 uzduotis". Isvestis su 50 studentu:
```
Vardas            Pavarde           Galutinis (Vid.) / Galutinis (Med.)
------------------------------------------------------------
Vardas1           Pavarde1          3.88               3.8
Vardas10          Pavarde10         4.19               3.2
Vardas11          Pavarde11         3.93               3.4
Vardas14          Pavarde14         2.49               2.2
Vardas26          Pavarde26         4.61               4.4
Vardas28          Pavarde28         4.17               4.2
Vardas31          Pavarde31         3.89               3.6
Vardas35          Pavarde35         2.97               3
Vardas37          Pavarde37         3.6                3.2
Vardas38          Pavarde38         4.73               4.2
Vardas39          Pavarde39         2.84               2.6
Vardas4           Pavarde4          3.19               3
Vardas40          Pavarde40         2.15               2.2
Vardas42          Pavarde42         4.17               3.8
Vardas43          Pavarde43         4.8                4
Vardas48          Pavarde48         2.49               2.2
Vardas49          Pavarde49         2.12               1.8
Vardas6           Pavarde6          3.65               3.2
Vardas8           Pavarde8          2.89               2.6

Patenkinami:
Vardas            Pavarde           Galutinis (Vid.) / Galutinis (Med.)
------------------------------------------------------------
Vardas12          Pavarde12         8.24               8.4 
Vardas13          Pavarde13         6.04               5.4 
Vardas15          Pavarde15         6.75               6 
Vardas16          Pavarde16         6.41               6.2 
Vardas17          Pavarde17         5.91               6.2 
Vardas18          Pavarde18         8.4                8.4 
Vardas19          Pavarde19         8.43               8.4 
Vardas2           Pavarde2          6.15               6.2
Vardas20          Pavarde20         7.87               7.6 
Vardas21          Pavarde21         7.36               7.2 
Vardas22          Pavarde22         6.47               6.6 
Vardas23          Pavarde23         6.83               6.8 
Vardas24          Pavarde24         6.04               5.4
Vardas25          Pavarde25         8.04               8.2 
Vardas27          Pavarde27         6.39               6.2
Vardas29          Pavarde29         5.23               5.2
Vardas3           Pavarde3          5.59               5.8 
Vardas30          Pavarde30         6.55               6.6
Vardas32          Pavarde32         5.09               5.2 
Vardas33          Pavarde33         6.25               5.8 
Vardas34          Pavarde34         5.36               4.8 
Vardas36          Pavarde36         8.91               9.2 
Vardas41          Pavarde41         6.6                6.2 
Vardas44          Pavarde44         6.4                6
Vardas45          Pavarde45         6.85               6.4 
Vardas46          Pavarde46         8.45               8.4 
Vardas47          Pavarde47         6.55               6.2 
Vardas5           Pavarde5          7.29               7.4
Vardas50          Pavarde50         5.05               4.6
Vardas7           Pavarde7          7.83               7.4 
Vardas9           Pavarde9          6.89               6.6 
```
