# MémoireManager — La mémoire des managers

> **Ne perdez plus jamais le fil de vos 1:1.**
> Suivi des collaborateurs, synthèses automatiques de réunions et agent IA qui rappelle les engagements.

SaaS freemium pour solopreneur français. Les livrables sont des pages HTML autonomes (zéro dépendance serveur), prêtes à héberger sur n'importe quel hébergement statique (GitHub Pages, Netlify, Vercel, OVH…).

---

## 📁 Contenu du dossier

| Fichier | Rôle |
|---|---|
| `index.html` | Landing page : hero, présentation des 3 fonctions, 3 offres tarifaires, formulaire EmailJS (essai gratuit) |
| `app-demo.html` | **Démo réelle** : espace de travail fonctionnel en JavaScript pur (localStorage), moteur de synthèse par règles, limite de l'offre Gratuite simulée |
| `README.md` | Ce fichier : architecture, positionnement, configuration |

---

## 🎨 Identité visuelle — « Espace de travail chaleureux »

**Consigne design respectée : 100 % distinct des templates existants.** Aucun fond sombre cyan/violet, aucune particule 3D, aucun émeraude/teal, aucun ambre/or, aucun bleu institutionnel.

- **Fond** : anthracite chaud `#14100d` (jamais de noir/bleu froid)
- **Accents** : corail `#ff6b4a` + tangerine `#ffa14a`
- **Texte** : ivoire `#f4ecdf` (et déclinaisons douces/faibles)
- **Typographie** : Fraunces (serif éditorial chaleureux) pour les titres, Outfit pour le corps
- **Architecture** : sidebar sombre façon espace de travail (logo, navigation, jauge de plan), hero split avec mockup d'application (fiches collaborateurs + filet de suivi 1:1), cartes très arrondies (rayon 20–26 px) avec ombres chaudes et lueurs corail/tangerine
- **Détail signature** : carte flottante « Agent IA · rappel automatique » animée en douceur dans le hero

---

## 📬 EmailJS — configuration réelle

Le formulaire d'essai gratuit (`index.html` → section `#essai`) envoie un **vrai** email via EmailJS. Aucun simulateur.

| Paramètre | Valeur |
|---|---|
| Service ID | `service_cy1ytdb` |
| Template ID | `template_xpo58cv` |
| Clé publique | `8Pui4ZEqxW2jRVF7h` |
| Payload | `{ site: "memoire-manager", name, email, question }` |

Le champ `site` permet de filtrer les leads par projet dans le tableau de bord EmailJS. La librairie est chargée en `<head>` (CDN jsDelivr) **avant** l'appel `emailjs.init(...)` — piège classique des formulaires morts évité. Gestion des états : validation (nom, format email), bouton « Envoi en cours… », message d'erreur réseau, écran de confirmation personnalisé.

> ⚠️ Ne pas déclencher d'envoi de test depuis la console pendant les vérifications : chaque envoi est un vrai lead.

---

## 🧪 Démo réelle (`app-demo.html`) — ce qui fonctionne

La démo est un vrai produit miniature, entièrement en JavaScript vanilla :

1. **Ajouter un collaborateur** (nom) → fiche créée avec avatar initiales, compteur d'équipe, jauge de plan dans la sidebar.
2. **Limite de l'offre Gratuite (3 collaborateurs)** : le 4ᵉ ajout est **bloqué** — message d'upgrade + bannière « Découvrir Pro » + toast. La jauge passe à 3/3.
3. **Créer un 1:1** avec les 3 champs (« Ce que tu as bouclé », « Ce que tu as dans le pipe », « Point de blocage ») + choix « dans X jours » pour le prochain rendez-vous.
4. **Synthèse automatique par règles** : le moteur découpe les phrases, les classe (avancées / actions à suivre / sujets à aborder) grâce à des lexiques français (verbes d'action, marqueurs de futur, marqueurs de blocage). Les blocages sont préfixés « Blocage : » et remontés en priorité.
5. **Prochain 1:1 « dans X jours »** : date française complète calculée (ex. « mercredi 26 août 2026 »), stockée sur la fiche du collaborateur.
6. **Actions cochables** : chaque engagement de la synthèse se coche (réalisée → barrée), l'état est persisté.
7. **Sauvegarde localStorage** : les collaborateurs, réunions, synthèses et cases cochées survivent au rechargement (clé `mm_v1`). Bouton « Réinitialiser la démo » pour revenir aux données d'exemple.
8. **Historique des 1:1** : toutes les synthèses sont reconsultables d'un clic.

**Données d'exemple** : 2 collaborateurs (Camille Rousseau, Karim Benali) avec un 1:1 chacun, pour montrer la valeur immédiatement.

> Note d'honnêteté produit : la démo utilise un moteur de synthèse **par règles** (zéro coût, fonctionne hors ligne). En production, le même pipeline est branché sur un LLM pour des synthèses plus riches — l'architecture du code (classification phrase par phrase) le permet sans refonte.

---

## 💰 Modèle freemium (affiché sur la landing)

| Offre | Prix | Contenu |
|---|---|---|
| **Gratuit** | 0 € | Jusqu'à 3 collaborateurs · suivi 1:1 · synthèses automatiques · réunions illimitées |
| **Pro** | 12 €/mois | Collaborateurs illimités · **agent IA de rappel** des engagements · synthèses enrichies par IA · historique + export CSV · rappels email/agenda |
| **Team** | 29 €/mois | Multi-équipes et rôles · **synthèses automatiques de toutes les réunions** · bot pour toute l'équipe · rappels pour tous les managers · support prioritaire |

Paiement par carte ou virement (facturation carte en cours de mise en place). Sans engagement.

---

## 🎯 Positionnement face à folotim.fr

### Ce qu'est Folotim
Folotim se positionne sur **la même promesse** : « la mémoire des managers », suivi des collaborateurs et des points 1:1, bot en réunion, synthèses automatiques, gratuit jusqu'à 3 collaborateurs. C'est donc le concurrent direct — et la preuve que le marché existe.

### L'angle différenciant de MémoireManager
Notre territoire n'est pas « noter », c'est **« faire aboutir »** :

1. **L'agent IA de rappel proactif** (offre Pro) — notre différence n°1.
   - Folotim aide à *préparer* et *retracer* le 1:1 ; MémoireManager **relance dans le temps** : chaque engagement est surveillé et rappelé à échéance, au manager **et** au collaborateur concerné (« relancer le client avant vendredi » → rappel J-2).
   - Le suivi ne s'arrête pas à la fin de la réunion : c'est la différence entre une *mémoire passive* (on consulte) et une *mémoire active* (elle vient à vous).
2. **Des synthèses orientées exécution** — notre différence n°2.
   - La synthèse n'est pas un compte rendu de plus : elle est structurée **actions à suivre (cochables) + sujets à aborder**, reliée automatiquement au prochain 1:1 planifié. Chaque synthèse alimente directement la fiche du collaborateur et le calendrier des rappels.
3. **Un modèle tarifaire clair** — Folotim affiche « Gratuit » sans lisibilité des paliers payants ; MémoireManager propose un freemium explicite (0 / 12 € / 29 €) avec un upgrade naturel : la limite de 3 collaborateurs est vécue dans la démo elle-même.

### Synthèse de positionnement
> « Folotim se souvient de vos réunions. **MémoireManager fait tenir vos engagements.** »

Angle marketing : « Le manager n'oublie plus rien, et ses collaborateurs non plus. » Cible : managers d'équipes de 2 à 50 personnes qui veulent ritualiser le 1:1 **et** voir les promesses tenues.

---

## 🚀 Prochaines étapes suggérées

1. Héberger sur GitHub Pages / Netlify (les deux fichiers sont statiques, aucun build requis).
2. Connecter un vrai domaine (`memoiremanager.fr`).
3. Brancher le moteur de synthèse sur un LLM (pipeline déjà pensé pour).
4. Mettre en place le paiement par carte (Stripe) pour les offres Pro/Team.
5. Ajouter la vraie authentification et le multijoueur (base de données) quand la demande le justifie.

---

*© 2026 MémoireManager — Fait avec soin en France.*
