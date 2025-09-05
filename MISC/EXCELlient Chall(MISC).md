## **EXCELlient Chall(MISC)**

## **Summary**

The workbook used formulas and named ranges instead of macros. The file assembles the flag from five named parts (Part0…Part4) which point at Calc0\!A5 … Calc4\!A5. By evaluating each Calc sheet cell (following the formulas and referenced cells) the final concatenation yields the flag: FLAG{SHEET\_SORCERY\_425}

## **Step 1 — Inspect workbook structure**

Open the workbook and list sheets and defined names (Excel → Formulas → Name Manager or programmatically).

The workbook contained named ranges:

Part0 → Calc0\!$A$5  
 Part1 → Calc1\!$A$5  
 Part2 → Calc2\!$A$5  
 Part3 → Calc3\!$A$5  
 Part4 → Calc4\!$A$5

The Flag sheet concatenates them:  
 A1 \= \=CONCATENATE(Part0,Part1,Part2,Part3,Part4)

## **Step 2 — Examine each `Calc` cell (the parts)Calc0\!A5**

##  Calc0\!A5  Formula: \=CHAR(70)\&CHAR(76)\&CHAR(65)\&CHAR(71)&"{"  CHAR(70)=F, CHAR(76)=L, CHAR(65)=A, CHAR(71)=G, then append {.  \=\> FLAG{

## Calc1\!A5  Formula: \=CHAR(B2)\&CHAR(C2)\&CHAR(D2)\&CHAR(E2)\&CHAR(F2)\&CHAR(G2)  Inspecting B2:G2 gives numeric codes \[83,72,69,69,84,95\] → S H E E T \_  \=\> SHEET\_

## Calc2\!A5  Formula uses many INDEX(A2:A100,n) wrapped in CHAR(...) to pick character codes from column A.  Indices used: \[8,2,3,4,5,3,6,7\]  Mapping to column A values:  index 8 → A9 → 83 → S  index 2 → A3 → 79 → O  index 3 → A4 → 82 → R  index 4 → A5 → evaluates to 99 → c  index 5 → A6 → 69 → E  index 3 → A4 → 82 → R  index 6 → A7 → 89 → Y  index 7 → A8 → 95 → \_  Concatenating gives: SORCERY\_

## Calc3\!A5  Formula: \=TEXT(45*45-1600,0)*  *45*45 \= 2025, 2025 \- 1600 \= 425  TEXT(...,0) → "425"  \=\> 425

## Calc4\!A5  Formula: \=CHAR(125) → }  \=\> }

## **Step 3 — Final assembly**

`Flag!A1` concatenates the five parts:

* Part0 → `FLAG{`

* Part1 → `SHEET_`

* Part2 → `SORCERY_`

* Part3 → `425`

* Part4 → `}`

Therefore final flag \= `FLAG{SHEET_SORCERY_425}`

