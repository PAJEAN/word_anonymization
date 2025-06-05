# Outil d'anonymisation de fichiers Word (.docx)

Cet outil permet d'anonymiser automatiquement le contenu de documents Word (.docx) en remplaçant les noms fournis par des codes anonymes.

---

## 🛠 Dépendances

Ce script utilise :

* `python-docx`

Installez les dépendances si besoin :

```bash
pip install python-docx
# ou
pip install -r requirements.txt
```

---

## 🚀 Utilisation

1. Ajouter les fichiers `.docx` à anonymiser dans le dossier `INPUT/`.
2. Lancer le script Python :

```bash
   python main.py
```

3. Les fichiers .docx anonymisés seront enregistrés dans le dossier `OUTPUT/`.

---

## 📁 Structure des fichiers et dossiers

* `INPUT/` : placez ici les fichiers `.docx` à anonymiser.
* `OUTPUT/` : les fichiers anonymisés seront générés ici.
* `ERROR/` : si une erreur survient, le fichier .docx source sera déplacé au sein de ce dossier.
* `NAMES.txt` : fichier contenant les noms à anonymiser.
* `main.py` : script d'anonymisation.
* `file.log` : fichier pour recencer les activités du script.

---

## 🧠 Fonctionnalités

* **Recherche et remplacement** des noms fournis dans une liste d'entrée par des codes anonymes (`[ANONYME_1]`, etc.).
* **Conservation du formatage** du document dans la mesure du possible.

* **Avertissement en cas d'ambiguïté** :
  * Le script signale lorsqu'un mot proche d'un nom (par exemple avec des majuscules ou accents différents) est détecté.
  * **Ces mots ne sont pas modifiés** mais listés pour vérification manuelle.

* **Vérification du formatage Word** : le script peut détecter des structures complexes ou des formats qui empêchent l'anonymisation et le signale.
  * Cette vérification **supprime le formatage temporairement** pour analyse, c'est pourquoi elle **n'est pas appliquée au fichier final**.

* Une liste des noms remplacés et leurs identifiants anonymes est affichée au sein de la console.

---

## ⚠️ Limitations

* L'outil a été testé uniquement sur des documents Word avec une structure simple.
* Certains éléments de formatage complexes dans Word (ex : noms éclatés en plusieurs blocs de texte avec du style) peuvent empêcher le remplacement.

---

## 📌 À noter

* Les noms à anonymiser doivent être fournis dans le fichier `NAMES.txt`.
* Aucun nom n'est remplacé sans correspondance exacte : les noms partiellement similaires sont **signalés mais non modifiés**.

---

## 📬 Exemple

Si le fichier `INPUT/rapport_medical.docx` contient :

```
Patient : Jean Dupont
```

Et que la liste de noms contient `"Jean Dupont"`, alors la sortie dans `OUTPUT/rapport_medical.docx` contiendra :

```
Patient : [ANONYME_1]
```

La correspondance sera indiquée directement dans la console :

```
------------------------------------------------------------
[CHECK] INPUT\rapport_medical.docx
------------------------------------------------------------
Jean Dupont → [ANONYME_1]
```

Voici un exemple d'affichage si une alerte est levée lors de l'anonymisation d'un fichier.

```
[FAIL]  INPUT\hut.docx
            Nom -> NOM // Le nom a été trouvé dans le document avec une casse différente
```