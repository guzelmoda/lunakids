# Guzel Yildiz Moda — Landing page pyjama

Landing page de vente (français + arabe) pour la boutique **Guzel Yildiz Moda**.
Produit : pyjama enfant en polaire, **199 DH** au lieu de 249 DH, commande via WhatsApp, paiement à la livraison au Maroc.

## Aperçu local

Le site est 100 % statique (HTML/CSS/JS). Deux options :

1. **Double-clic** sur `index.html` (fonctionne, mais les liens WhatsApp et les polices se comportent mieux via un serveur).
2. **Serveur local** (recommandé) :

```powershell
cd C:\Users\HP\luna-kids
python -m http.server 5501
```

Puis ouvrir http://localhost:5501/ dans le navigateur.

## Fichiers

```
luna-kids/
├─ index.html          # Structure + contenu français par défaut + balises SEO
├─ styles.css          # Styles responsive + mode RTL arabe
├─ script.js           # Galerie, formulaire, messages WhatsApp, dictionnaire FR/AR
├─ assets/
│  ├─ pijama-rose.jpg  # Fille en pyjama rose
│  ├─ pijama-vert.jpg  # Fille en pyjama vert sauge
│  ├─ pijama-blanc.jpg # Fille en pyjama blanc crème
│  ├─ pijama-gris.jpg  # Garçon en pyjama gris perle
│  └─ favicon.svg
└─ qa/                 # Captures et rapports de tests (non nécessaires en production)
```

## Fonctionnement de la commande

Le formulaire ne paie rien en ligne : il valide le nom, le téléphone marocain, la ville, la taille et la couleur, puis ouvre WhatsApp avec un message pré-rempli contenant :

- le produit et la couleur choisie,
- la taille et la quantité,
- le total calculé (199 DH × quantité),
- le nom, le téléphone et la ville du client.

Le message est généré **dans la langue active** (français ou arabe).

## Modifier les informations essentielles

### Numéro WhatsApp

Le numéro est en format international **212718181080** (07 18 18 10 80 sans le 0 initial).

À remplacer aux endroits suivants :

- `index.html` : tous les liens `https://wa.me/212718181080` (boutons, FAQ, footer).
- `script.js` : constante `WA_NUMBER = "212718181080"`.

### Prix

- `index.html` : textes visibles `199 DH` / `249 DH`, balises SEO et données structurées JSON-LD.
- `script.js` : constantes `PRICE = 199` et `OLD_PRICE = 249` (calcul du total et message WhatsApp).

### Textes et traductions

- Le **français** est le contenu par défaut écrit directement dans `index.html`.
- Les traductions sont dans `script.js` : objets `T_FR` et `T_AR`.
- Chaque texte porte un attribut `data-i18n="clé"` ; pour modifier un libellé, changez la valeur correspondante dans les deux dictionnaires (et le HTML pour le français).

### Langue par défaut

- La page s'ouvre en **français** par défaut.
- Si le navigateur est configuré en arabe et qu'aucun choix n'a été enregistré, la page s'ouvre en **arabe**.
- Le choix AR/FR est mémorisé dans le navigateur (`localStorage`, clé `gy-lang`).
- Le bouton **FR | ع** se trouve dans l'en-tête ; en arabe, la page passe automatiquement en RTL.

### Couleurs et tailles

- Couleurs : `rose`, `vert`, `blanc`, `gris` — images et libellés dans `script.js` (`COLOR_IMG`, dictionnaires).
- Tailles : 2–3, 4–5, 6–7, 8–9, 10–11 ans — valeurs des radios dans `index.html`, correspondance arabe dans `script.js` (`SIZE_KEY`).

### Images

Remplacez les fichiers dans `assets/` en conservant les mêmes noms, ou mettez à jour les chemins dans `index.html` et `script.js`.
Format conseillé : JPG, environ 1350 × 1200 px, moins de 300 Ko par image pour un chargement rapide.

## Mettre en ligne

Le site fonctionne sur tout hébergement statique :

- **Netlify / Vercel** : glissez-déposez le dossier `luna-kids`.
- **GitHub Pages** : poussez les fichiers puis activez Pages.
- **Hébergement classique (cPanel, o2switch…)** : envoyez `index.html`, `styles.css`, `script.js` et le dossier `assets/` à la racine du site (ou dans un sous-dossier).

Aucune base de données ni serveur Node n'est nécessaire.

## À vérifier avant de lancer des publicités

Les éléments suivants sont des **hypothèses commerciales** à confirmer avec la boutique :

- livraison **24–48 h** dans les grandes villes et 2–4 jours ailleurs ;
- **échange de taille gratuit sous 7 jours** (article non porté, emballage d'origine) ;
- paiement à la livraison disponible **partout au Maroc** ;
- caractère **hypoallergénique** de la polaire (à ne conserver que si le fabricant le confirme) ;
- frais de livraison : actuellement non affichés (précisés sur WhatsApp).

Les avis clients (« Salma B. », « Yassine E. », « Imane K. »), la note **4,9/5** et les **127 avis vérifiés** sont des **exemples de démonstration**. Remplacez-les par de vrais témoignages (avec accord des clients) avant toute campagne publicitaire.

Le compte à rebours de l'offre se termine chaque jour à minuit : c'est un ressort d'urgence visuel, pas une date de fin réelle. Adaptez-le à votre politique commerciale.

## Tests effectués

- Affichage FR et AR (RTL) sur desktop 1440 px, mobile 390/360/320 px.
- Aucun débordement horizontal.
- Changement de langue instantané, mémorisé après rechargement.
- Galerie photo, changement de couleur, total automatique, validation du téléphone marocain.
- FAQ (une seule réponse ouverte à la fois), barre fixe mobile, bouton WhatsApp flottant.
- Messages WhatsApp FR et AR générés avec les bonnes informations et le bon numéro.

Captures et rapports : dossier `qa/` (`final-*.png`, `final-results.json`, `i18n-results.json`).
