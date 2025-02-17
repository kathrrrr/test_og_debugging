# test_og_debugging




---
# 1. Introduktion til Softwaretest
## Hvad er softwaretestning?
Softwaretest sikrer, at vores kode fungerer korrekt og håndterer fejl på en kontrolleret måde.  

Der findes **tre testmetoder**:  
**Sort box test** – Test af **funktionalitet** uden at kende den interne kode.  
**Hvid box test** – Test af **kode og struktur** for at finde fejl.  
**Grå box test** – En blanding af de to; tester både funktionalitet og noget af koden.  

### Eksempel
En test af et **login-system** kan være:
- **Sort box test**: Tester login med korrekte/ukorrekte oplysninger.  
- **Hvid box test**: Vi tester login ved at kigge direkte på koden, f.eks. hvordan SQL-forespørgslen håndteres.  
- **Grå box test**: Tester mysql-kommandoerne direkte i phpmyadmin.  

---
Vi kan teste koden ved hvid box test ved brug af f.x unittest og doctest.
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

# 4. Debugging med Breakpoints 
### Hvad er et breakpoint?
- Et **stop-punkt i koden**, hvor vi kan inspicere værdier.  
- Bruges i **VS Code**, eller med `pdb` i terminalen.  

### **Brug af `pdb` til debugging**
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



---

## **Logbog: **
Skriv i logbog om hvad du lærte om
**Sort, hvid og grå box test**   
**`unittest`** 
**`doctest`** 
**Breakpoints** 
**Logging**   
Skriv også hvilke værtøjer du fandt mest nytting. 

---

