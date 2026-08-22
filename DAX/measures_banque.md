# DAX Measures — Analyse Bancaire

## 1. CapitauxP
```dax
CapitauxP = SUMX(
    FILTER(
        Bilan,
        Bilan[Nature]="Passif" &&
        Bilan[Objet]="C1" ||
        Bilan[Objet]="C2"
    ),
    Bilan[Montant]
)
```

## 2. Total Actif
```dax
Total actif = SUMX(
    FILTER(Bilan,Bilan[Nature]="Actif"),
    Bilan[Montant]
)
```

## 3. Total Dépôts
```dax
Total_Depots = SUMX(
    FILTER(
        Bilan,
        Bilan[Nature]="Passif" &&
        Bilan[Objet]="T2"
    ),
    Bilan[Montant]
)
```

## 4. Total Prêts
```dax
Total_Pret = SUMX(
    FILTER(
        Bilan,
        Bilan[Nature]="Actif" &&
        Bilan[Objet]="T1"
    ),
    Bilan[montant]
)
```

## 5. Trésorerie
```dax
Trésorie = SUMX(
    FILTER(
        Bilan,
        Bilan[Nature]="Tresorerie" &&
        Bilan[Objet]="T10"
    ),
    Bilan[Montant]
)
```

## 6. Résultat
```dax
Resultat = SUMX(
    FILTER(Bilan,Bilan[Objet]="R"),
    Bilan[Montant]
)
```

## 7. Résultat Net
```dax
RNet = SUMX(
    FILTER(
        Bilan,
        Bilan[Nature]="Passif" &&
        CONTAINSSTRING(
            Bilan[Designation],
            "Résultat net"
        )
    ),
    Bilan[Montant]
)
```

## 8. LDR — Loan to Deposit Ratio
```dax
LDR = DIVIDE([Total actif],[Total_Depots],0)
```

## 9. LTAR — Loan to Asset Ratio
```dax
LTAR = DIVIDE([Total_Pret],[Total actif],0)
```

## 10. ROA — Return on Assets
```dax
ROA = DIVIDE([Resultat],[Total actif],0)
```

## 11. ROE — Return on Equity
```dax
ROE = DIVIDE([RNet],[CapitauxP],0)
```