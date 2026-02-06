# Mérési Jegyzőkönyv

**Téma:** Műveleti erősítő alapkapcsolások vizsgálata (Invertáló erősítő)  
**Készítette:** Bekényi Dávid  
**Dátum:** 2026. január 29.  
**Helyszín:** Laboratórium

---

## 1. Mérési feladat
A mérés célja a **TL071** típusú műveleti erősítő működésének vizsgálata invertáló alapkapcsolásban, **NI myDAQ** adatgyűjtő eszköz segítségével. A feladat során megvizsgáljuk az áramkör feszültségerősítését és átviteli karakterisztikáját.

<img width="961" height="535" alt="kapcsolas" src="https://github.com/user-attachments/assets/f5630b76-4dfe-4dc5-8373-ef704dac2e93" />

## 2. Felhasznált eszközök

| Eszköz / Alkatrész | Típus / Érték | Mennyiség | Megjegyzés |
| :--- | :--- | :---: | :--- |
| Adatgyűjtő kártya | **NI myDAQ** | 1 db | Tápellátás, jelgenerátor, oszcilloszkóp |
| Műveleti erősítő | **TL071** | 1 db | JFET bemenetű, kis zajú Op-Amp |
| Ellenállás | **100 kΩ** | 3 db | Visszacsatolás, bemenet, kompenzálás |
| Próbapanel | Breadboard | 1 db | - |
| Összekötő huzalok | - | - | - |

## 3. Elméleti összefoglaló

Az invertáló erősítő kapcsolásban a visszacsatoló ellenállás ($R_f$) a kimenet és az invertáló bemenet (-) közé csatlakozik. A bemeneti jel ($U_{be}$) egy soros ellenálláson ($R_{in}$) keresztül jut az invertáló bemenetre. A nem invertáló bemenetet (+) földpotenciálra kötjük (gyakran egy kompenzáló ellenálláson keresztül).

Az ideális műveleti erősítő feszültségerősítése ($A_u$):

$$A_u = \frac{U_{ki}}{U_{be}} = - \frac{R_f}{R_{in}}$$

Jelen mérésben $R_f = 100\text{k}\Omega$ és $R_{in} = 100\text{k}\Omega$, így az elméleti erősítés:

$$A_u = - \frac{100\text{k}\Omega}{100\text{k}\Omega} = -1$$

Ez egységnyi erősítést jelent 180°-os fázisdordítás mellett.

## 4. Mérési összeállítás
![IMG_2537](https://github.com/user-attachments/assets/5a040d72-e62e-4898-9a96-82a70d61bd9d)


A kapcsolást a próbapanelen az alábbiak szerint állítottuk össze:

* **Tápellátás (NI myDAQ):**
    * $V+$ $\rightarrow$ TL071 7-es láb (+15V)
    * $V-$ $\rightarrow$ TL071 4-es láb (-15V)
    * $AGND$ $\rightarrow$ Közös föld
* **Áramkör:**
    1.  **$R_1$ (100 kΩ):** A jelgenerátor kimenete és a TL071 2-es (invertáló) lába között.
    2.  **$R_2$ (100 kΩ):** A TL071 2-es lába és a 6-os (kimenet) láb között (visszacsatolás).
    3.  **$R_3$ (100 kΩ):** A TL071 3-as (nem invertáló) lába és a Föld (GND) között (feszültségeltolódás kompenzálása).
* **Műszerek csatlakoztatása:**
    * **AO0 (Analog Output):** Szinuszos gerjesztő jel ($R_1$ bemenetére).
    * **AI0 (Analog Input 0):** Bemeneti jel vizsgálata.
    * **AI1 (Analog Input 1):** Kimeneti jel vizsgálata (TL071 6-os láb).

## 5. Mérési eredmények

<img width="523" height="591" alt="generator" src="https://github.com/user-attachments/assets/6dabf40f-58eb-47a7-80f9-92528f5523f6" />
<img width="1082" height="745" alt="szkop" src="https://github.com/user-attachments/assets/3aaa3bff-bd78-4b35-83fa-d92c63db83ab" />



### 5.1 Időtartománybeli vizsgálat
*Beállítás:* $f = 1 \text{kHz}$ szinuszjel, $U_{pp} = 2 \text{V}$ (csúcstól-csúcsig).

| Paraméter | Mért érték |
| :--- | :--- |
| Bemeneti feszültség ($U_{be, pp}$) | 1.98 V |
| Kimeneti feszültség ($U_{ki, pp}$) | 1.97 V |
| Fáziseltolódás | ~180° |

**Számított erősítés a mérés alapján:**

$$A_{mért} = \frac{1.97 \text{V}}{1.98 \text{V}} \approx -0.995$$

A mérési hiba a névleges értékekhez képest elhanyagolható, a tűréshatáron belül van.

### 5.2 Bode-diagram (Frekvencia átvitel)
A bemeneti frekvencia változtatásával vizsgáltuk az erősítés csökkenését.

| Frekvencia ($f$) | Bemenet ($U_{be}$) | Kimenet ($U_{ki}$) | Erősítés (dB) |
| :--- | :--- | :--- | :--- |
| 100 Hz | 2.0 V | 2.0 V | 0 dB |
| 1 kHz | 2.0 V | 1.99 V | -0.04 dB |
| 10 kHz | 2.0 V | 1.95 V | -0.22 dB |
| 100 kHz | 2.0 V | 1.41 V | -3.01 dB |

*Megjegyzés: A -3dB-es törésponti frekvencia kb. 100 kHz-nél jelentkezett.*

## 6. Kiértékelés

A mérés során sikeresen összeállítottunk egy invertáló erősítőt a TL071 IC és a rendelkezésre álló 100 kΩ-os ellenállások segítségével.

1.  **Működés:** Az áramkör az elvárásoknak megfelelően invertálta a jelet ($180^{\circ}$-os fázisforgatás).
2.  **Erősítés:** A beállított ellenállásarányok ($100\text{k} / 100\text{k}$) révén az erősítés mértéke egységnyi volt ($A \approx -1$).
3.  **Eszközhasználat:** Az NI myDAQ eszköz szoftveres oszcilloszkópjával a jelalakok zajmentesek és jól követhetőek voltak.

A mérést sikeresnek nyilvánítom.

---
