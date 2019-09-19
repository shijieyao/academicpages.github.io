<h2>Concordance Coefficient</2>

- Cohen Kappa: two annotators
  - ```k = (Pr(a) - Pr(e)) / (1 - Pr(e))```
  - where Pr(e) is the probability of agreeing with each other by accident; Pr(a) is the actual probability of choosing same label\

- Fleiss Kappa: more than two annotators
  - ```k = (P - Pe) / (1 - Pe)```
  - where P is the actual concordance; Pe is the expected concordance
  - `Pc` is the percentage of each tag c among all tags
  - `Pi` is the concordance of each annotator with the other
  - ```Pi = (sum(ac)) / (a(a-1))``` where `a` is the total number of tags, `ac` is the number of c tag annotated
  - ```P = average(Pi)```
  - ```Pe = sum(Pc ^ 2)```