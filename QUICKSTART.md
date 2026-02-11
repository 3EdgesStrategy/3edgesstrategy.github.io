# 🚀 Démarrage rapide - Blog 3Edges

## ✅ Ce qui est déjà fait

- ✅ Hugo installé et configuré
- ✅ Thème PaperMod installé
- ✅ Support LaTeX pour les équations
- ✅ Workflow GitHub Actions configuré
- ✅ Premier article exemple créé
- ✅ Serveur de développement testé

## 📋 Checklist de publication

### 1️⃣ Configurer Git (1 minute)

```bash
cd ~/3edges/3edges-blog

git config user.name "3Edges"
git config user.email "TON_EMAIL_ANONYME@example.com"
```

### 2️⃣ Créer le repository GitHub (2 minutes)

1. Se connecter sur github.com avec le compte **3EdgesStrategy**
2. Cliquer sur "New repository"
3. Nom du repo : **`3edges.github.io`** (exactement ce nom !)
4. Repository **public**
5. **Ne pas** initialiser avec README
6. Créer le repository

### 3️⃣ Pousser le code (1 minute)

```bash
cd ~/3edges/3edges-blog

# Initialiser git
git init

# Ajouter tous les fichiers
git add .

# Premier commit
git commit -m "Initial blog setup with Hugo and PaperMod"

# Lier au repository
git remote add origin https://github.com/3edgesstrategy/3edges.github.io.git

# Pousser
git branch -M main
git push -u origin main
```

### 4️⃣ Activer GitHub Pages (1 minute)

Sur GitHub.com :
1. Aller dans ton repository
2. **Settings** (onglet en haut)
3. **Pages** (menu à gauche)
4. **Source** → Sélectionner **"GitHub Actions"**
5. Sauvegarder

### 5️⃣ Attendre le déploiement (2-3 minutes)

1. Aller dans l'onglet **"Actions"** du repository
2. Tu verras le workflow "Deploy Hugo site to Pages" en cours
3. Attendre qu'il devienne vert ✅
4. Le site sera accessible sur : **https://3edges.github.io**

---

## 🎉 C'est tout ! Ton blog est en ligne !

### Tester en local avant de publier

```bash
cd ~/3edges/3edges-blog
hugo server -D -p 1314
# Ouvrir http://localhost:1314
```

### Publier le premier article

```bash
# 1. Éditer l'article
nano ~/3edges/3edges-blog/content/posts/analyse-volatilite-crypto.md

# 2. Changer "draft: true" en "draft: false"

# 3. Ajouter les images
cp ~/Documents/freqtrade-docker/python_utils/volatility_term_structure_all.png \
   ~/3edges/3edges-blog/static/

# 4. Commiter et pousser
cd ~/3edges/3edges-blog
git add .
git commit -m "Publish first article: volatility analysis"
git push origin main

# 5. Attendre 2-3 minutes → Article en ligne !
```

### Créer un nouvel article

```bash
cd ~/3edges/3edges-blog
hugo new posts/mon-nouvel-article.md
# Éditer le fichier créé dans content/posts/
```

---

## 📚 Documentation complète

- **SETUP_COMPLETE.md** : Configuration détaillée
- **COMMANDS.md** : Toutes les commandes utiles
- **README.md** : Documentation du projet

## 🆘 Besoin d'aide ?

- **Hugo ne démarre pas ?** → `hugo version` pour vérifier l'installation
- **Git ne pousse pas ?** → Vérifier l'URL du remote avec `git remote -v`
- **Le site ne se déploie pas ?** → Vérifier l'onglet "Actions" sur GitHub
- **Les équations ne s'affichent pas ?** → Vérifier `math: true` dans l'article

---

**Temps total estimé : 7-10 minutes** ⏱️

**Prêt ? Go ! 🚀**
