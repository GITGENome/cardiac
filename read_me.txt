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
      - restect 0 est plus correle avec le persone pas malade. Le valeur 2 est tres bizzard.
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

                                                            ***
Machine learning

1. The library of lazypredict was used to chose the models with the best balanced score. Independed of the lazypredict choice
  I always test MPL, SVC, RandomForest

2. Before the model improvement whole dataset was splited in X, y, X_apres, y_apres. This small franction of data is supposed to 
  be used after model is complet

3. For each model the best scaler was selected

4. For each combination of scaler+model ML the search of the best hyperparameters was done

5. The models with the lowest false negative results were chosen to be used in staking model ensemble

6. The search of the best final estimator for the model ensemble was done. The LogisticRegression was chosen.
  LogisticRegression as a final estimator was also tested with changed weight of classes to eliminate false negative results

7. Final model was tested with X_apres, y_apres. The score is 0.89

8. Final model was fitted with the whole dataset and was dumped to use in application

                                                            ***
Adjustments

1. Exclution of cp (chest pain) from final model
When model was tested in application it was imposible to understant connection of chest pain. According to client the value of chest pain
correspond to the pain level, but with our visuals we cannot see the correlation. 0 - has a strong correlation with disease, while 1, 2 - is not
3 - has a strange impact. 
However presence of chest pain is a strong indicator of heart disease it was excluded, because it's not a reason of disease but more a consequences and cannot be used as an EARLY factor of disease identification

2. False negetive results.
After research of scaler and best hyperparameters models where it was possible to change the weight of class was tested to eliminate 
false negative result. This feature is not used in final model because client didn't give us defenitive information about ill and healthy persone. It was our guesse. Also it was impossible to use model with change class weight in model ensemble. 
Model ensemble allows to increase the score better and eliminate more false negative that just changing of class weight

3. Qualitive/quantitive feature. 
Some feature which was definied as categorical (cp, fbs, sex, slope, resteg, exang, ca, thalasemmia) were transformed into object columns 
in X to be treated with OneHotEncoder rather than scaler adapted for quantitive values.
This was excluded in final model because it had no impact on model performance, score and number of false negative results were the same. 
However it complicated model functioning/training because some rare classes were hard to include in train/test split
I think those rare classes are outliers, but according to our client it is not, so we decided to keep it and treat all values as quantitive

   

