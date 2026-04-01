# Exercice 2 — Gestion d'un conflit Git via GitHub

## Objectif

Créer deux branches à partir de `main`, introduire un conflit en modifiant la même ligne dans `.github/pull_request_template.md`, puis résoudre ce conflit directement depuis l'interface GitHub.

---

## Étapes

### 1. Créer les deux branches depuis `main`

S'assurer d'être sur `main` et à jour :

```bash
git checkout main
git pull origin main
```

Créer la première branche :

```bash
git checkout -b conflict1
```

Revenir sur `main` puis créer la seconde branche :

```bash
git checkout main
git checkout -b conflict2
```

---

### 2. Introduire le conflit

Les deux branches doivent modifier **la même ligne** dans `.github/pull_request_template.md`.

#### Sur `conflict/branch-1`

```bash
git checkout conflict1
```

Modifier la ligne concernée dans `.github/pull_request_template.md`, par exemple changer :

```
- [ ] Les changements ont été testés localement (soon conflict)
```

en :

```
- [ ] Les changements ont été testés localement (big conflict)
```

Committer et pousser :

```bash
git add .
git commit -m "feat: conflict1"
git push origin conflict1
```

#### Sur `conflict2`

```bash
git checkout conflict2
```

Modifier la **même ligne** avec un contenu différent, par exemple :

```
- [ ] Les changements ont été testés localement (big conflict)
```

Committer et pousser :

```bash
git add .
git commit -m "feat: conflict2"
git push origin conflict2
```

---

### 3. Créer les Pull Requests sur GitHub

1. Ouvrir une PR de `conflict1` → `main` et la **merger en premier**
2. Ouvrir une PR de `conflict2` → `main`

La seconde PR affichera un conflit car la même ligne a été modifiée différemment.

---

### 4. Résoudre le conflit depuis GitHub

1. Sur la PR de `conflict2`, cliquer sur **"Resolve conflicts"**
2. L'éditeur GitHub affiche les marqueurs de conflit :

```
<<<<<<< conflict/branch-2
- [ ] Les changements ont été testés localement (soon conflict)
=======
- [ ] Les changements ont été testés localement (big conflict)
>>>>>>> main
```

3. Supprimer les marqueurs et conserver la version souhaitée, par exemple :

```
- [ ] Les changements ont été testés localement
```

4. Cliquer sur **"Mark as resolved"** puis **"Commit merge"**
5. La PR peut maintenant être mergée normalement

---

## Résultat

Le conflit a été résolu sans ligne de commande, directement dans l'interface GitHub. Le fichier `.github/pull_request_template.md` sur `main` contient la version finale choisie lors de la résolution.
