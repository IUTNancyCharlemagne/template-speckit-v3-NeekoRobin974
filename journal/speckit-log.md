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
- Fusion directe via l'IA sans étape de superposition locale → Raison : L'IA aurait moins de guidage structurel (silhouette) sur le résultat attendu, risquant des fusions moins cohérentes avec les deux Pokémon choisis.
- Utilisation d'un paramètre `strength` plus élevé (> 0.8) → Raison : Le résultat s'éloignerait trop des Pokémon originaux, perdant l'aspect "fusion" reconnaissable.

**Prompts clés utilisés (cités ou reformulés) :**
> /speckit.constitution Je veux développer une application mobile "PokéFusion" pour fusionner deux sprites de Pokémon. L'application superpose d'abord les deux images choisies à 50% d'opacité en local. Ce "brouillon" est ensuite envoyé à l'API Img2Img d'Hugging Face (modèle : stable-diffusion-v1-5/stable-diffusion-v1-5) avec un paramètre strengt d'environ 0.65 pour lisser l'image et générer la créature (Pokémon) finale. Modifie le fichier @.specify/memory/constitution.md en séparant bien la logique mobile de l'appel à l'IA.

**Difficultés rencontrées / ajustements effectués :**
- Nécessité de clarifier la distinction entre "brouillon local" et "génération finale" dans les principes du projet pour assurer une architecture découplée.

**Degré de validation par l'étudiant :**
1. Résultat accepté sans modification
