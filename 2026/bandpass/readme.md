# MÉRÉSI JEGYZŐKÖNYV

**Intézmény:** Miskolci SZC Kandó Kálmán Informatikai Technikum  
**Helyszín:** Miskolc, V3 Labor  
**Dátum:** 2026. 02. 02.

---

## 1. A mérés adatai

* **Mérést végezte:** Vass Viktor
* **Mérés tárgya:** Aktív sávszűrő vizsgálata (LM324)
* **Alkalmazott mérőrendszer:** NI myDAQ (National Instruments) – Bode Analyzer

---

## 2. A mérés célja
LM324 típusú műveleti erősítővel felépített aktív sávszűrő (Bandpass Filter) áramkör vizsgálata. A szűrő rezonanciafrekvenciájának ($f_0$) és az ott mérhető feszültségerősítésnek ($A_0$) meghatározása, valamint az átviteli karakterisztika (Bode-diagram) felvétele.

---

## 3. Felhasznált alkatrészek

A kapcsolás egy műveleti erősítős, többszörös visszacsatolású (vagy ahhoz hasonló topológiájú) sávszűrő.

| Pozíciószám | Alkatrész | Érték (Kapcsolási rajz) | Funkció |
| :--- | :--- | :--- | :--- |
| **IC1** | LM324 | - | Műveleti erősítő (Quad Op-Amp) |
| **R1** | Ellenállás | **220 Ω** | Bemeneti osztó / szűrő tag |
| **R2** | Ellenállás | **220 Ω** | Szűrő tag (Föld felé) |
| **R3** | Ellenállás | **11,91 kΩ** | Visszacsatoló ellenállás |
| **C1** | Kondenzátor | **470 nF** | Csatoló/Szűrő kapacitás |
| **C2** | Kondenzátor | **470 nF** | Csatoló/Szűrő kapacitás |

<img width="720" height="516" alt="image" src="https://github.com/user-attachments/assets/ec496cc4-c921-4841-9855-5d04b10f6f24" />    

## Az áramkör kivitelezése és a kapcsolási rajz módosításai

A mérési feladat elvégzése során az eredeti elvi kapcsolási rajzhoz képest az alábbi módosításokat eszközöltük a fizikai megvalósításkor:

### Földelési topológia módosítása
Az LM324 műveleti erősítő bekötésénél a földelési pont kialakítását megváltoztattuk.
* **Eredeti állapot:** A kapcsolási rajz szerint az IC 11-es lába (negatív tápfeszültség/VEE) és a 3-as láb (nem invertáló bemenet) közösítve csatlakozott a földeléshez.
* **Módosítás:** A 11-es láb és a földelés közötti eredeti összeköttetést ebben a formában megszüntettük. A földelési pontot közvetlenül az R2 ellenállás és az IC 3-as lába közötti szakaszra helyeztük át.

**A módosítás indoklása:**
A változtatásra a stabilabb működés és a zajcsökkentés érdekében volt szükség. A nem invertáló bemenet (3-as láb) közvetlen, önálló földelése biztosítja, hogy a bemeneti referenciafeszültség "tisztább" legyen, és ne kerüljön rá a tápfeszültség visszatérő ágán (11-es láb) esetlegesen megjelenő zavarjel vagy feszültségesés. Ez a huzalozási elrendezés javítja a jel-zaj viszonyt.

### Alkatrészek értékei
A megépített áramkörben felhasznált passzív komponensek (ellenállások és kondenzátorok) értékei kismértékben eltérnek az elvi kapcsolási rajzon feltüntetett névleges értékektől.
* **Ok:** A laboratóriumi készletben nem álltak rendelkezésre pontosan az eredeti rajzon szereplő értékű alkatrészek, így azokat a legközelebbi szabványos értékű elemekkel helyettesítettük. A működést ez érdemben nem befolyásolja, de a mérési eredmények kiértékelésénél a ténylegesen beépített értékeket vettük figyelembe.

### A módosított kapcsolás:      
<img width="1097" height="699" alt="image" src="https://github.com/user-attachments/assets/f05dcf01-35aa-4bf9-9ee4-b03c838b9d4c" />

---

## 4. Elméleti számítások

Az áramkör egy sávszűrő, amely egy adott frekvenciatartományt enged át, míg az alacsonyabb és magasabb frekvenciákat csillapítja.

A rezonanciafrekvencia ($f_0$) elméleti meghatározása az alkalmazott passzív alkatrészek ($R$, $C$) értékeitől függ. A kapcsolás topológiája alapján a középfrekvencia közelítőleg:

$$f_0 = \frac{1}{2\pi C} \sqrt{\frac{R_1 + R_2}{R_1 R_2 R_3}}$$

**Várt viselkedés:**
A kimeneti jel amplitúdója a rezonanciafrekvencián ($f_0$) éri el a maximumot.
---

## 5. Mérési eredmények

A méréshez az NI myDAQ *Bode Analyzer* műszerét használtam 10 Hz és 20 kHz közötti tartományban.

**Mért értékek a kurzor alapján:**
* **Rezonanciafrekvencia ($f_0$):** 309,68 Hz
* **Erősítés a csúcson ($Gain$):** 29,17 dB
* **Fázis ($Phase$):** 0° (Invertáló jellegre utal a rezonancia közelében)

<img width="924" height="740" alt="image" src="https://github.com/user-attachments/assets/a1582458-42de-4354-b486-a8ed26c3d856" />  

---

## 6. Kiértékelés

A mérés során az LM324-es IC-vel felépített kapcsolás sávszűrőként viselkedett. A Bode-diagramon jól látható a kiemelés a 300 Hz-es tartományban.

* A **29,17 dB-es erősítés** jelentős feszültségerősítést jelent a rezonanciafrekvencián ($A_u \approx 28,7$).
* A fázisgörbe menete igazolja a frekvenciafüggő fázistolást, amely a rezonancia környezetében éles változást mutat.
* Az áramkör szelektíven emeli ki a ~310 Hz körüli jeleket, míg a 10 Hz-es és 10 kHz-es tartományban a jelet jelentősen csillapítja (negatív dB értékek a grafikon szélein).

**Aláírás:**

__________________________
**Bekényi Dávid**
