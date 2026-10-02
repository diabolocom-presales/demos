---
name: page-demo-chatbot
description: Génère une page web de démonstration personnalisée aux couleurs et au vocabulaire d'un prospect, à partir du template espace client, pour y tester le chatbot. Gère aussi le cycle complet jusqu'à la publication sur GitHub Pages (récapitulatif, validation, nommage du dossier, ajout à la page d'accueil, push). À utiliser dès que l'utilisateur parle de préparer une démo, une page de démo ou de test de chat, un site de démo, un espace client fictif, ou donne le brief d'un prospect (nom, secteur, activité) en vue d'une présentation commerciale.
---

# Générateur de page de démo chatbot

Adapter `assets/template_chatpage.html` (dans le dossier de ce skill) au brief d'un prospect. Le livrable est **un fichier HTML autonome**, prêt à être ouvert dans un navigateur pour une démo commerciale, puis publié sur GitHub Pages une fois validé.

## Point de départ obligatoire

Toujours partir de `assets/template_chatpage.html`, jamais d'une page écrite de zéro. La mise en page (alignements, espacements, grilles) est déjà réglée : elle ne se retouche pas.

## Structure : 10 bandeaux

La page est découpée en 10 bandeaux, repérés dans le template par des commentaires `<!-- BANDEAU n/10 : ... -->`. Chaque bandeau est adaptable, dans les limites indiquées :

| # | Bandeau | Ce qui s'adapte | Ce qui ne bouge pas |
|---|---------|-----------------|---------------------|
| 1 | **Header** | Logo client (seul, sans nom de marque à côté), entrées du menu (4 à 6), nom de l'utilisateur + initiales de l'avatar | Structure du header |
| 2 | **Alerte démo** | Rien | Phrase conservée telle quelle, en haut de page (mention Diabolocom incluse, ne jamais supprimer) |
| 3 | **Salutation** | Prénom, sous-titre (« Voici un aperçu de vos… »), libellé du bouton | Le bouton reste fonctionnel |
| 4 | **Blocs n°1** | Les 3 blocs : liste principale (3 lignes : intitulé, catégorie, statut, montant), encart promo (titre + accroche + image), compteur de progression | Toujours 3 blocs, disposition 2 colonnes |
| 5 | **Image** | Titre de section (dernier mot en accent) + visuel pleine largeur | Format de l'image |
| 6 | **Blocs n°2** | Titre de section + **exactement 4 tuiles** (icône + libellé) | Grille de 4 |
| 7 | **Texte descriptif** | Paragraphe entier, réécrit dans le vocabulaire du client | Longueur comparable (6 à 10 phrases) |
| 8 | **Blocs n°3** | Titre de section + **4 tuiles puis 3 tuiles** d'assistance | Grilles 4 + 3 |
| 9 | **Footer 1** | Pays / langue | Pas de logo à cet endroit (déjà présent en header) |
| 10 | **Footer 2** | Liens du menu bas de page | Mention `© Diabolocom, 2026` conservée |

Ajouter ou retirer une tuile est possible si le brief l'exige, mais il faut alors conserver une grille équilibrée (4, ou 4+3) : sinon la mise en page se casse.

## Déroulé

### 1. Lire le brief

Le brief contient au minimum : **nom du client, secteur, type d'activité**. En déduire :

- **Le persona** : à qui appartient cet espace client ? (assuré, abonné, acheteur B2B, technicien, agent…)
- **Le vocabulaire** : reprendre les termes exacts du métier. Un assureur parle de *contrat*, *sinistre*, *garantie*, *échéance*, pas de *commande* ni de *ticket*. Un SAV parle de *retour*, *garantie*, *numéro de série*. Une équipe commerciale parle de *devis*, *opportunité*, *compte*.
- **Les objets listés dans le bandeau 4** : commandes, contrats, tickets, factures, devis, expéditions… avec des statuts crédibles (*En cours d'instruction*, *Expédié*, *Clôturé*).
- **Les rubriques d'aide (bandeau 8)** : celles qu'aurait réellement ce client.

Chercher rapidement la charte graphique réelle du client (couleurs officielles) si son nom est connu, pour coller au maximum à son identité visuelle plutôt que d'inventer une palette.

### 2. Générer une première version et présenter le récapitulatif

Produire tout de suite une première version du HTML, avec des placeholders (`placehold.co`) là où des images manquent. Ne jamais bloquer sur des questions avant d'avoir montré quelque chose.

Présenter ensuite un récapitulatif, dans cet ordre :

- **Les 10 bandeaux** : uniquement leur nom et leur contenu tel qu'il apparaît dans cette version (ex. « Bandeau 4 — Blocs n°1 : liste des 3 derniers sinistres, encart promo assistance routière, compteur de fidélité »). **Ne pas** décrire ce qui a changé par rapport au template ou à une version précédente, seulement l'état actuel, comme une photo de la page.
- **Inspirations** : sites ou chartes de référence utilisés (marque elle-même si connue, sinon acteurs du même secteur).
- **Couleurs utilisées** : les 5 couleurs principales avec leur rôle.
- **Images à fournir** : lister ce qui est encore en placeholder, avec taille (grande/moyenne/petite) et format attendus.
- **Code d'intégration du chatbot** : demander systématiquement, en même temps que les images manquantes, le script fourni par le client au format `<script src="https://fr2.chat.diabolocom.com/UUID/config.js"></script>`. Rappeler à l'utilisateur qu'il doit aussi penser à ajouter l'URL `https://diabolocom-presales.github.io/demos/*` dans la liste des pages cibles (déclencheur) du chatbot côté plateforme Diabolocom : sans cela, le chatbot ne s'affichera pas sur la page une fois publiée.
- **Points de vigilance** : uniquement si un risque existe (voir « Vigilance : lisibilité du logo »). Omettre cette ligne s'il n'y a rien à signaler.

Ne pas proposer de nom de dossier ni parler de publication à ce stade : ça viendra seulement après réception des images.

### 3. Valeurs par défaut

Si le brief ne les précise pas :

- nom d'utilisateur affiché : **Louis Dubois** (avatar `LD`, salutation « Bonjour Louis ») ;
- nom de la compagnie : **Dunder Mifflin** ;
- logo : placeholder généré (`https://placehold.co/...`), signalé comme à remplacer ;
- pays : France ; année du copyright : celle en cours.

### 4. Adapter les couleurs

Ne modifier que le bloc `:root` en tête du `<style>`, sauf demande explicite de l'utilisateur portant sur un élément hors `:root` (ex. « je veux le header en telle couleur »). Dans ce cas, relier l'élément concerné à une variable existante ou nouvelle plutôt que de coder une couleur en dur ailleurs :

- `--accent` : couleur principale du client. Elle pilote les liens, le survol des tuiles, les mots en accent des titres et la barre de progression ;
- `--tag1`, `--tag2`, `--tag3` : pastilles de catégorie du bandeau 4 ;
- `--footer` / `--footer-txt` / `--footer-muted` / `--footer-line` : couleur de fond et couleurs de texte du header (bandeau 1) et du footer (bandeau 10), qui partagent toujours les mêmes valeurs pour rester visuellement cohérents comme un seul bandeau haut/bas ;
- `--card`, `--bg` : uniquement si le client a une identité claire (fond clair ou sombre). `--card` est aussi la couleur de fond du footer 1 (`.locale-bar`, bandeau 9).

**Règle de décision pour le header/footer, selon le logo du client :**

- **Logo à dominante blanche/claire** (pensé pour un fond sombre) → comportement par défaut du template : `--footer` reste une couleur foncée de la charte, `--footer-txt:#ffffff`, `--footer-muted:#cdd4db`, `--footer-line:#222222`.
- **Logo à dominante colorée ou foncée** (pas blanc) → passer le header/footer en blanc : `--footer:#ffffff`, `--footer-line` en gris clair (ex. `#e2e6ea`), et surtout **mettre les textes en couleur pour qu'ils ressortent** plutôt qu'en noir plat : `--footer-txt` en couleur de marque foncée ou en `--accent` (pour le nom de marque et le lien actif), `--footer-muted` en gris foncé lisible (ex. `#5a6672`) pour les liens de menu au repos.

Vérifier le contraste : texte clair sur les cartes sombres, texte foncé sur les fonds clairs. Un accent trop pâle sur fond sombre devient illisible.

**5 couleurs principales à définir :**

- une couleur à fort contraste pour le header et le footer (`--footer`) : basée sur la charte du client ;
- une couleur claire pour le fond (`--bg`) : reprend la couleur du header en très, très clair ;
- une couleur claire pour le bandeau texte descriptif (`--banner`) : reprend la couleur du fond, légèrement plus foncée ;
- une couleur un peu foncée pour les blocs (`--card`) : reprend la couleur du header/footer mais plus claire (+20 %) ;
- une couleur d'appel (`--accent`) : contraste avec le reste, s'oppose à la charte du client pour ressortir sur les surlignages et les survols.

### Vigilance : lisibilité du logo

Le header et le footer (bandeau 10) appliquent la règle de décision ci-dessus selon la dominante du logo (clair → fond foncé, coloré/foncé → fond blanc). Le footer 1 n'affiche plus de logo : il n'y a donc plus de risque de contraste à cet endroit. Le seul emplacement à surveiller reste le header/footer, déjà couvert par la règle de décision.

### 5. Images et icônes

- N'utiliser que des URLs plausibles et stables : `https://cdn-icons-png.flaticon.com/512/...` pour les icônes (elles héritent d'un filtre qui les affiche en blanc : choisir des icônes monochromes pleines, pas des illustrations en couleurs). Réutiliser en priorité les icônes déjà validées dans le template ou dans une démo précédente plutôt que d'en inventer de nouvelles.
- Ne jamais inventer une URL de photo produit ou de logo réel : la demander à l'utilisateur, ou utiliser un placeholder explicite (`placehold.co`) en attendant.
- Chaque image conservée depuis le template mais hors-sujet doit être remplacée ou signalée.

### 6. Interdits

- Ne pas toucher au CSS de structure (`.grid`, `.card`, `.help-grid`, marges, espacements en cm).
- Ne pas supprimer le bandeau 2 (mention site de démonstration) ni le copyright, **y compris la mention Diabolocom** : elle reste obligatoire dans chaque page HTML de démo (bandeau 2 et footer).
- Ne pas supprimer le marqueur `<!-- SNIPPET CHATBOT ... -->` en fin de fichier. Une fois le script d'intégration reçu (voir étape 2), l'insérer juste après ce marqueur, toujours en tout dernier élément avant `</body>` : ne rien ajouter après.
- Pas de dépendance externe autre que les images : le fichier doit s'ouvrir hors ligne, mise en page intacte.
- Pas de fausse promesse réglementaire (montants, mentions légales, garanties précises) : rester générique.

### 7. Réception des images : nouvelle version + nom de dossier proposé

Quand l'utilisateur fournit les images manquantes :

1. Régénérer le HTML en les intégrant (plus aucun placeholder d'image restant, sauf celles explicitement non fournies).
2. Présenter cette nouvelle version avec le même format de récapitulatif que l'étape 2 (bandeaux = nom + contenu, sans mention de ce qui a changé).
3. Proposer le **nom du dossier de publication**, au format `secteur_business_datedepublication` (voir section 8), et l'annoncer clairement.
4. Demander la validation : « Cette version et ce nom de dossier vous conviennent ? »

### 8. Validation et publication

- **Si l'utilisateur valide tel quel** → passer directement à la publication (ci-dessous).
- **Si l'utilisateur demande une modification** (contenu, couleur, nom de dossier…) → l'appliquer, puis enchaîner directement sur la publication, sans redemander une nouvelle validation.

**Publication** (dépôt `diabolocom-presales/demos`, publié via GitHub Pages) :

- **Nom de dossier** : `secteur_business_datedepublication`, tout en minuscules, sans accents ni espaces (remplacés par `_`). Le secteur et le business sont chacun un ou deux mots courts. La date est au format `jjmoisaa` (jour sans zéro inutile, mois en toutes lettres en français, année sur 2 chiffres), ex. `sport_sav_19aout26`, `assurance_marketing_3dec26`. Le dossier est créé à la racine du dépôt.
- Le fichier à l'intérieur du dossier s'appelle toujours `index.html`.
- **Page d'accueil** : la racine du dépôt contient un `index.html` qui liste les démos sous forme de cartes. Il n'est pas généré automatiquement : après ajout du dossier, ajouter une carte dans la grille `.grid`, en copiant le bloc d'une carte existante, avec le numéro suivant, `href="./nom_du_dossier/"` et le nom du dossier comme libellé.
- Committer avec un message descriptif (ex. « Ajout de la démo assurance_marketing_3dec26 ») et pousser sur la branche de travail ou sur `main` selon la consigne de l'utilisateur.
- Toujours renvoyer à la fin le lien racine **https://diabolocom-presales.github.io/demos/** (qui liste toutes les démos), ainsi que le lien direct vers la nouvelle démo : `https://diabolocom-presales.github.io/demos/nom_du_dossier/`.
