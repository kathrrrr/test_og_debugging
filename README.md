# test_og_debugging




---
# 1. Introduktion til Softwaretest
## Hvad er softwaretest?
Softwaretest sikrer, at vores kode fungerer korrekt og håndterer fejl på en kontrolleret måde.  

Der findes **tre testmetoder**:  
**Black box test** – Test af **funktionalitet** uden at kende den interne kode.  
**White box test** – Test af **kode og struktur** for at finde fejl.  
**Grey box test** – En blanding af de to; tester både funktionalitet og noget af koden.  

### Eksempel
En test af et **login-system** kan være:
- **Black box test**: Tester login med korrekte/ukorrekte oplysninger.  
- **White box test**: Vi tester login ved at kigge direkte på koden, f.eks. hvordan SQL-forespørgslen håndteres.  
- **Grey box test**: Tester mysql-kommandoerne direkte i phpmyadmin.  

---
Black box test dokumenteres i et skema. Her ses et skema for Sort Box Test for Login-system

| **Test ID** | **Input (Brugernavn, Kodeord)** | **Forventet Output** | **Faktisk Output** | **Bestået?** |
|------------|-------------------------------|----------------------|--------------------|-------------|
| **T1** | `"admin", "1234"` | "Login successful" | "Login successful" | Ja |
| **T2** | `"admin", "wrongpass"` | "Invalid username or password" | "Invalid username or password" | Ja |
| **T3** | `"nonexistent", "password"` | "Invalid username or password" | "Invalid username or password" | Ja ||
| **T4** | `"" , ""` (Tom input) | "Invalid username or password" | "Invalid username or password" | Ja |

---
Vi kan teste koden ved white box test ved brug af f.x unittest og doctest.
# 2. `unittest` – Struktureret testning 
### Hvad er `unittest`?
- Et indbygget test-framework i Python.  
- Giver struktureret testning med testklasser og assertions.  
- Tester funktioner, moduler og systemer i større projekter.  

### Eksempel
```python
import unittest

def add(x, y):
    return x + y

class TestMathFunctions(unittest.TestCase):
    def test_add(self):
        self.assertEqual(add(2, 3), 5)
        self.assertEqual(add(-1, 1), 0)

if __name__ == "__main__":
    unittest.main()
```

### Øvelse 1: Skriv din egen test
1. Lav en funktion `multiply(x, y)`, der ganger to tal.  
2. Skriv en `unittest` for at teste den.  
3. Kør testen og se resultatet.  

---

# 3. `doctest` – Hurtig test og dokumentation
### Hvad er `doctest`?
- Lader dig **skrive tests direkte i docstrings**.  
- Bruges til **hurtige tests** og til at sikre, at dokumentation er korrekt.  

### Eksempel
Betragt denne kode
```python
def add(x, y):
    """
    Returnerer summen af x og y.
    
    """
    return x + y

```

Her kan vi i docstringen indsætte test

```python
def add(x, y):
    """
    Returnerer summen af x og y.
    
    >>> add(2, 3)
    5
    >>> add(-1, 1)
    0
    """
    return x + y

if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

### Øvelse 2: Brug `doctest`
1. Lav en funktion `subtract(x, y)`, der trækker to tal fra hinanden.  
2. Tilføj en `doctest` til funktionen.  
3. Kør `doctest` og se resultatet.  

---

# 4. Debugging med `print()`  

## Hvad er debugging med `print()`?
En af de **mest grundlæggende metoder** til at debugge kode er at indsætte `print()`-kommandoer for at **se, hvad der sker i programmet**.

**Fordele ved `print()` debugging:**  
Enkel og hurtig at bruge.  
Kræver ingen ekstra værktøjer.  
Kan bruges overalt i koden.  

**Ulemper ved `print()` debugging:**  
Bliver hurtigt rodet i større projekter.  
Kræver manuel fjernelse af `print()` efter debugging.  
Giver ingen avanceret fejlhåndtering.  

---

## Eksempel: Debugging med `print()`
Lad os sige, vi har en funktion, der dividerer to tal, men den fejler nogle gange:

```python
def divide(a, b):
    print(f"DEBUG: a = {a}, b = {b}")  # Debug print
    return a / b

print(divide(10, 2))  # OK
print(divide(10, 0))  # Fejl! Division med nul
```
**Output:**
```
DEBUG: a = 10, b = 2
5.0
DEBUG: a = 10, b = 0
ZeroDivisionError: division by zero
```
**Her bruger vi `print()` til at se værdierne af `a` og `b`, inden fejlen opstår.**

---

## **Øvelse: Find en fejl med `print()`**
**Fejlen:** Følgende funktion giver ikke det forventede resultat.  
**Din opgave:** Brug `print()` til at finde fejlen.  

```python
def calculate_total(prices):
    total = 0
    for price in prices:
        total = price  # Fejl! Skal være total += price
    return total

print(calculate_total([10, 20, 30]))  # Forventet: 60, men hvad returneres?
```
**Tilføj `print()` i funktionen for at se, hvordan `total` ændrer sig!**  

---

## Hvornår bør man bruge `print()` debugging?
Hurtige fejlfindingssessioner.  
Når du tester en **mindre funktion**.  
Når du arbejder i et **simpelt script** uden debugging-værktøjer.  

**Men:** I større projekter er **logging og breakpoints bedre** til systematisk debugging!  

---

**Nu ser vi, hvordan breakpoints kan gøre debugging mere effektiv!** 


---



# 5. Debugging med Logging 
### Hvad er logging?
- **Logging** giver os information om, hvad der sker i programmet.  
- Det bruges til **fejlsporing**, **performance-målinger**, og **overvågning**.  

### Eksempel på logging
```python
import logging

logging.basicConfig(level=logging.DEBUG)

def divide(a, b):
    logging.debug(f"divide({a}, {b}) called")
    if b == 0:
        logging.error("Division by zero!")
        return None
    return a / b

print(divide(10, 2))
print(divide(10, 0))
```
### Eksempel på logging i en fil
```python
import logging

logging.basicConfig(filename='example.log',level=logging.DEBUG)

def divide(a, b):
    logging.debug(f"divide({a}, {b}) called")
    if b == 0:
        logging.error("Division by zero!")
        return None
    return a / b

print(divide(10, 2))
print(divide(10, 0))
```
### **Logging niveauer**
| Niveau  | Beskrivelse |
|---------|------------|
| `DEBUG` | Detaljeret debugging-info |
| `INFO` | Generel information |
| `WARNING` | Noget ser mærkeligt ud |
| `ERROR` | En fejl er opstået |
| `CRITICAL` | Kritisk fejl, der stopper programmet |

### Øvelse 4: Brug logging
1. Lav en funktion `safe_divide(a, b)`, der deler tal.  
2. Brug `logging` til at logge kald, fejl og resultater.  

---
# 6. Debugging med Breakpoints 
### Hvad er et breakpoint?
- Et **stop-punkt i koden**, hvor vi kan inspicere værdier.  
- Bruges i **VS Code**, eller med `pdb` i terminalen.  


### **Brug af `pdb` til debugging**
pdb står for python debugger.
```python
import pdb

def faulty_function(x):
    pdb.set_trace()  # Sætter breakpoint
    result = x + "10"  # Fejl: int + str
    return result

faulty_function(5)
```
### Øvelse 3: Debugging med breakpoints
1. Indsæt et breakpoint i en funktion.  
2. Kør koden og inspicér variablerne.  

---


---

## **Logbog: **
Skriv i logbog om hvad du lærte om
**black box, Grey box, White box test**   
**`unittest`** 
**`doctest`** 
**Breakpoints** 
**Logging**   
Skriv også hvilke værtøjer du fandt mest nytting. 

---

