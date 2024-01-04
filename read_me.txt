Pas de valeurs manquant.
Peut-etre il y a un doublon, mais sans id de patint c'est impossible de savoir

Il y a 14 col numerique, la majoritè avec les valeurs vategorique qui étaient transformés/factorizé

                                                            ***

Les colone avec les valeur continues:
  trestbps
  chol
  thalach
  oldpeak

Les valeurs categorique:
  cp (chest pain): de 0 a 4. Le formateur a dit que c'est la severité de douleur, je lui ne crois pas, car sur le lmplot 
      la ligne s'approche aux gens malades avec le ca=0
  fbs (fasting blood sugar): 0 et 1 (normal/pas normal)
  restecg (ECG resting): 0, 1 et pour 4 persones c'est 2. Juste une persone parmi ceux-ci est malade
  exang (exercise-induced angine): 0 et 1.
  slope(change is ST segment slope under exercise): 0, 1, 2 - 1 le plus associe avec la maladie
  ca(Number of Major Vessels Colored by Fluoroscopy): 0-4, 4 - majorite de gens sont pas malades, tandi que la valeur plus grand associe avec la       maladie
  thalasemia - me posse le problem, car c'est une maladie genetique et dans la base de donnée il y a enormenet de gens malades. Les chiffre            correspondent a maladie ou ils sont alèatoires?

                                                            ***

Visualisation:
  boxplot avec malade/pas malade. Le bon difference malade/sain est pour le variable d'age, exang(douleur pendant exercice), 
      oldpeak, ca (visualisation de vessau de coeur)
  lmplot (l'éstimation de regression): 
      - les hommes plus sensibles avec l'age que les femmes
      - les pression de sang plus hommes le factor de risk plus grand pendant le moynne age
      - plus haut cholesterol a impact plus grand chez homme
      - la possibilité de developer frequence cardiac plus haut a très fort correlation avec le risk de maladie diminué
      - cp a très bizard correlation avec la maladie, IL FAUT LE FAIRE COMME GET DUMMIES! 
  pairplot
  distplot - les memes conclutions qu'avec lmplot et plus
      - 0 oldpeak a grand association avec les sains
      - ca 0 a la correlation avec les sains

                                                            ***

Statistique
    Normalité
      il y a quelques variable avec la distribution n'est pas normal: le cholesterol, l'age, thalach (exercise-induced heartbeat), slope.
      cela peut explique pourquoi il n'y a pas de correlation entre la maladie et le cholesterol
    test chi2 été utilisé pour éstimer de difference de valeur categoric. Il n'y a pas d'impact de fbs (fasting blood glucose)
    ANOVA test pour determiner la depandence de maladies et les valerus numirique continues

                                                            ***

PCA
No utility in decomposer. Le choix de deux composant peut expliquer juste 0.33 de variabilite de data. 

