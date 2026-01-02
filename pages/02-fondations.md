---
layout: center
class: text-center
---

# 📜 Rappel historique

<div class="mt-12 text-2xl space-y-8">
  <v-click>
    <div class="opacity-80">
      D'où vient Git ?
    </div>
  </v-click>
  
  <v-click>
    <div class="opacity-80">
      Pourquoi a-t-il révolutionné le développement ?
    </div>
  </v-click>
  
  <v-click>
    <div class="opacity-80">
      Comment fonctionne-t-il <strong>vraiment</strong> ?
    </div>
  </v-click>
</div>

<div v-click class="mt-16 text-lg opacity-60">
  Retour aux fondations pour mieux comprendre
</div>

<!--
Note orale:
- Transition depuis l'introduction
- Annoncer qu'on va revenir aux bases
- Créer de l'intérêt pour la suite
-->


---
layout: two-cols-header
class: text-center
---

# L'ère centralisée : SVN / CVS

<h2 class="mb-12">Avant Git</h2>

::left::

<div class="text-left">
  <ul>
    <li v-click="2">
      <strong>Serveur unique</strong> (SPOF - Single Point of Failure)
    </li>
    <li v-click="3">
      <strong>Dépendance au réseau</strong> pour chaque opération
    </li>
    <li v-click="4">
      <strong>Pas de sauvegarde locale</strong> complète
    </li>
    <li v-click="5" class="mt-4">
      <strong>Problème</strong> : Si le serveur tombe, tout s'arrête
    </li>
  </ul>
</div>

::right::

<v-click at="1">

```mermaid
graph TB
  Server[🖥️ Serveur Central<br/>SVN/CVS]
  Client1[💻 Client 1]
  Client2[💻 Client 2]
  Client3[💻 Client 3]
  
  Server -->|checkout| Client1
  Server -->|checkout| Client2
  Server -->|checkout| Client3
  Client1 -->|commit| Server
  Client2 -->|commit| Server
  Client3 -->|commit| Server
  
  style Server fill:#8b1e1e
  style Client1 fill:#004a45
  style Client2 fill:#004a45
  style Client3 fill:#004a45
```

</v-click>

<style>
  .two-cols-header {
    text-align: center;
  }
</style>

<!--
Note orale:
- Expliquer le problème du SPOF
- Montrer la dépendance au réseau
- Transition vers la solution distribuée
-->

---
layout: default
class: text-center
---

# Linus Torvalds et la Puissance du Distribué

<div class="text-2xl mt-8 space-y-6">
  <v-click>
    <div>
      <div class="font-bold text-3xl">Nécessité pour le noyau Linux</div>
      <div class="text-lg opacity-80 mt-2">Des milliers de contributeurs, besoin de performance</div>
    </div>
  </v-click>
  
  <v-click>
    <div>
      <div class="font-bold text-3xl">Concept révolutionnaire</div>
      <div class="text-lg opacity-80 mt-2">Chaque clone est une <strong>sauvegarde complète</strong></div>
    </div>
  </v-click>
  
  <v-click>
    <div>
      <div class="font-bold text-3xl">Avantages</div>
      <div class="text-lg opacity-80 mt-2">
        - Travail hors ligne<br>
        - Pas de serveur central<br>
        - Performance locale
      </div>
    </div>
  </v-click>
</div>

<!--
Note orale:
- Raconter brièvement l'histoire de la création de Git
- Insister sur le concept distribué
- Montrer les avantages pratiques
-->

---
layout: two-cols-header
class: text-center
---

# Le Modèle Distribué de Git

::left::

<div class="text-left space-y-4 mt-8">
  <v-click>
    <div>
      <div class="font-bold text-xl">📦 Chaque clone est complet</div>
      <div class="text-sm opacity-80 mt-1">Historique entier du projet</div>
    </div>
  </v-click>
  
  <v-click>
    <div>
      <div class="font-bold text-xl">✅ Pas de SPOF</div>
      <div class="text-sm opacity-80 mt-1">Si le serveur tombe, on continue</div>
    </div>
  </v-click>
  
  <v-click>
    <div>
      <div class="font-bold text-xl">🔄 Échanges flexibles</div>
      <div class="text-sm opacity-80 mt-1">Push/pull avec remote ou entre devs</div>
    </div>
  </v-click>
  
  <v-click>
    <div>
      <div class="font-bold text-xl">⚡ Travail hors ligne</div>
      <div class="text-sm opacity-80 mt-1">Commits, branches, merge localement</div>
    </div>
  </v-click>
</div>

::right::

<v-click>

```mermaid
graph TB
    Remote[📦 Remote]
    Dev1[💻 Dev 1]
    Dev2[💻 Dev 2]
    Dev3[💻 Dev 3]
    
    Remote <-->|push/pull| Dev1
    Remote <-->|push/pull| Dev2
    Remote <-->|push/pull| Dev3
    Dev1 -.-> Dev2
    Dev2 -.-> Dev3
    
    style Remote fill:#8b1e1e
    style Dev1 fill:#004a45
    style Dev2 fill:#004a45
    style Dev3 fill:#004a45
```

</v-click>

<style>
  .two-cols-header {
    text-align: center;
  }
</style>

<!--
Note orale:
- Montrer la différence avec le modèle centralisé
- Insister sur le fait que chaque clone est complet
- Expliquer qu'on peut travailler sans serveur central
- Mentionner les échanges directs possibles entre développeurs
-->

---
layout: two-cols-header
class: text-center
---

# Git stocke des Snapshots, pas des Deltas

<h3 class="opacity-80 mb-4">Comprendre le modèle de stockage de Git</h3>

::left::

<div class="text-left text-sm">
  <v-click>
    <div class="font-bold text-xl mb-2 text-red-600">❌ SVN : Modèle Delta</div>
    <div class="space-y-2">
      <div>
        <div class="font-semibold text-xs">Version initiale :</div>
        <code class="text-xs">File.txt (contenu complet)</code>
      </div>
      <div>
        <div class="font-semibold text-xs">Version 2 :</div>
        <code class="text-xs">+ ligne 5: "nouveau code"</code>
      </div>
      <div>
        <div class="font-semibold text-xs">Version 3 :</div>
        <code class="text-xs">- ligne 3 | + ligne 8</code>
      </div>
      <div class="mt-2 p-2 bg-red rounded">
        <div class="font-bold text-xs">⚠️ Problème :</div>
        <div class="text-xs opacity-80">Rejouer toutes les modifications depuis v1</div>
      </div>
    </div>
  </v-click>
</div>

::right::

<div class="text-left text-sm">
  <v-click>
    <div class="font-bold text-xl mb-2 text-green-600">✅ Git : Modèle Snapshot</div>
    <div class="space-y-2">
      <div>
        <div class="font-semibold text-xs">Commit 1 (abc123) :</div>
        <code class="text-xs">File.txt (v1 complète)</code>
      </div>
      <div>
        <div class="font-semibold text-xs">Commit 2 (def456) :</div>
        <code class="text-xs">File.txt (v2 complète)</code>
      </div>
      <div>
        <div class="font-semibold text-xs">Commit 3 (ghi789) :</div>
        <code class="text-xs">File.txt (v3 complète)</code>
      </div>
      <div class="mt-2 p-2 bg-green rounded">
        <div class="font-bold text-xs">✨ Avantage :</div>
        <div class="text-xs opacity-80">Accès instantané sans reconstruction</div>
      </div>
    </div>
  </v-click>
</div>

<v-click>

<div class="p-3 bg-blue rounded text-left mt-4">
  <div class="font-bold text-sm mb-1">💡 En réalité : Git optimise avec la compression</div>
  <div class="text-xs opacity-80">
    Git utilise des <strong>pack files</strong> pour compresser et dédupliquer les données identiques. 
    Le modèle conceptuel reste un snapshot, mais le stockage est optimisé !
  </div>
</div>

</v-click>

<style>
  .two-cols-header {
    text-align: center;
  }
  
  .two-cols-header code {
    background: rgba(0,0,0,0.1);
    padding: 2px 4px;
    border-radius: 3px;
  }
</style>

<!--
Note orale:
- SVN stocke la version initiale puis les différences (deltas)
- Git prend un "snapshot" complet à chaque commit
- Accès direct à n'importe quelle version sans reconstruction
- Git optimise en arrière-plan avec la compression (pack files)
- C'est pourquoi Git est si rapide pour les opérations locales
-->

---
layout: two-cols-header
---

# Sous le capot : Blob, Tree, Commit

<h3 class="opacity-80 mb-2">Les 3 objets fondamentaux de Git</h3>

::left::

<div class="text-left text-sm space-y-2">
  <v-click>
    <div class="p-2 bg-purple rounded">
      <div class="font-bold text-base mb-1">📄 Blob (Binary Large Object)</div>
      <div class="text-xs space-y-0.5">
        <div>• Stocke le <strong>contenu d'un fichier</strong></div>
        <div>• Compressé avec zlib</div>
        <div>• Identifié par SHA-1 du contenu</div>
        <div class="opacity-90 mt-1">
          <code>git hash-object fichier.txt</code>
        </div>
      </div>
    </div>
  </v-click>
  
  <v-click>
    <div class="p-2 bg-teal rounded">
      <div class="font-bold text-base mb-1">📁 Tree (Arbre)</div>
      <div class="text-xs space-y-0.5">
        <div>• Représente un <strong>répertoire</strong></div>
        <div>• Liste des fichiers et sous-dossiers</div>
        <div>• Référence les Blobs et autres Trees</div>
        <div class="opacity-90 mt-1">
          Comme un <code>ls -l</code> versionné
        </div>
      </div>
    </div>
  </v-click>
  
  <v-click>
    <div class="p-2 bg-blue rounded">
      <div class="font-bold text-base mb-1">💾 Commit (Snapshot)</div>
      <div class="text-xs space-y-0.5">
        <div>• Pointe vers un <strong>Tree racine</strong></div>
        <div>• Métadonnées : auteur, date, message</div>
        <div>• Référence au(x) commit(s) parent(s)</div>
        <div class="opacity-90 mt-1">
          C'est le "snapshot" du projet
        </div>
      </div>
    </div>
  </v-click>
</div>

::right::

<v-click>

<div class="mermaid-small">

```mermaid
graph TD
    Commit[💾 Commit<br/>abc123]
    Tree[📁 Tree<br/>def456]
    Blob1[📄 Blob<br/>ghi789<br/>app.js]
    Blob2[📄 Blob<br/>jkl012<br/>style.css]
    
    Commit -->|pointe vers| Tree
    Tree -->|contient| Blob1
    Tree -->|contient| Blob2
    
    style Commit fill:#3b82f6,color:#fff
    style Tree fill:#14b8a6,color:#fff
    style Blob1 fill:#a855f7,color:#fff
    style Blob2 fill:#a855f7,color:#fff
```

</div>

</v-click>

<v-click>

<div class="text-xs mt-2 p-2 bg-gray rounded text-left">
  <div class="font-bold mb-1">🔑 Principe clé :</div>
  <div>Chaque objet est immuable et identifié par son SHA-1. Si le contenu change, le hash change !</div>
</div>

</v-click>

<style>
  .two-cols-header {
    text-align: center;
  }
  
  .two-cols-header code {
    background: rgba(255,255,255,0.2);
    padding: 1px 4px;
    border-radius: 3px;
    font-size: 0.7em;
  }
  
  .bg-purple, .bg-teal, .bg-blue, .bg-gray {
    color: white;
  }
  
  .mermaid-small svg {
    max-height: 280px;
    font-size: 11px;
  }
  
  .mermaid-small .nodeLabel {
    font-size: 10px !important;
  }
</style>

<!--
Note orale:
- Blob : contenu pur du fichier, pas de nom ni métadonnées
- Tree : comme un répertoire, lie noms de fichiers et blobs
- Commit : snapshot complet avec historique (parent)
- Tous immuables : si on change 1 caractère, nouveau SHA-1
- C'est ce modèle qui rend Git si puissant et fiable
-->

