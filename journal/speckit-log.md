# Journal de développement

> **Projet :** PokéFusion
> **Étudiant :** Prénom Nom — BUT S6 AppDevMobile 2025-2026
> **Agent IA utilisé :** Gemini CLI

---

<!-- Les entrées suivantes sont générées automatiquement par votre agent à chaque fin de phase.
     Ne pas supprimer ni modifier les entrées existantes. -->

---
### Phase : constitution — 2026-03-16 18:08

**Décisions prises :**
- Séparation stricte de la logique de superposition locale (50% opacité) et de l'appel à l'API Hugging Face. Justification : Garantit un retour visuel immédiat pour l'utilisateur ("brouillon") et facilite le test indépendant des composants.
- Utilisation du modèle `stable-diffusion-v1-5` avec un paramètre `strength` de 0.65. Justification : Permet de lisser la fusion tout en conservant la structure des silhouettes originales des Pokémon.
- Adoption d'une approche "Mobile-First Local Processing" comme principe fondamental. Justification : Optimise les ressources réseau et améliore l'expérience utilisateur en traitant les étapes préliminaires en local.

**Alternatives écartées :**
- Fusion directe via l'IA sans étape de superposition locale → Raison : L'IA aurait moins de guidage structurel (silhouette) on le résultat attendu, risquant des fusions moins cohérentes avec les deux Pokémon choisis.
- Utilisation d'un paramètre `strength` plus élevé (> 0.8) → Raison : Le résultat s'éloignerait trop des Pokémon originaux, perdant l'aspect "fusion" reconnaissable.

**Prompts clés utilisés (cités ou reformulés) :**
> /speckit.constitution Je veux développer une application mobile "PokéFusion" pour fusionner deux sprites de Pokémon. L'application superpose d'abord les deux images choisies à 50% d'opacité en local. Ce "brouillon" est ensuite envoyé à l'API Img2Img d'Hugging Face (modèle : stable-diffusion-v1-5/stable-diffusion-v1-5) avec un paramètre strengt d'environ 0.65 pour lisser l'image et générer la créature (Pokémon) finale. Modifie le fichier @.specify/memory/constitution.md en séparant bien la logique mobile de l'appel à l'IA.

**Difficultés rencontrées / ajustements effectués :**
- Nécessité de clarifier la distinction entre "brouillon local" et "génération finale" dans les principes du projet pour assurer une architecture découplée.

**Degré de validation par l'étudiant :**
1. Résultat accepté sans modification

---
### Phase : specify — 2026-03-16 18:27

**Décisions prises :**
- Définition de trois User Stories prioritaires : (P1) Brouillon local, (P2) Génération AI, (P3) Gestion d'erreurs. Justification : Permet de découper le développement en étapes testables indépendamment, en commençant par le coeur de l'interaction utilisateur.
- Inclusion de critères de succès mesurables (ex: génération AI en moins de 20s). Justification : Permet d'évaluer objectivement la performance de l'application et de l'intégration API.
- Spécification des cas limites comme l'absence de sprite API ou les images locales trop grandes. Justification : Anticipe les problèmes de mémoire sur mobile et les limitations de la PokéAPI pour assurer la robustesse de l'MVP.

**Alternatives écartées :**
- Inclusion immédiate d'un système de sauvegarde Cloud → Raison : Trop complexe pour un MVP, la priorité est donnée à la génération locale et à l'appel IA.
- Utilisation exclusive de PokéAPI → Raison : L'ajout des images locales augmente l'engagement utilisateur en permettant de fusionner ses propres captures.

**Prompts clés utilisés (cités ou reformulés) :**
> Rédige les spécifications de l'MVP de PokéFusion (en Flutter). L'UI doit inclure un écran pour sélectionner 2 Pokémon (via PokéAPI ou des images en locales), un aperçu de la superposition à 50% d'opacité en local, et un bouton "Fusionner". Prévois un écran de résultat avec un indicatieur de chargement pendant l'appel à l'API Hugging Face, ainsi que la gestion des erreurs.

**Difficultés rencontrées / ajustements effectués :**
- Ajustement des paramètres de l'API Hugging Face (strength 0.65) pour équilibrer créativité et fidélité, comme demandé dans la constitution.

**Degré de validation par l'étudiant :**
1. Résultat accepté sans modification
