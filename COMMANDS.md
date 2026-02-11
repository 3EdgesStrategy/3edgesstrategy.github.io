# Commandes utiles pour le blog

## 🚀 Démarrage rapide

### Configuration Git (à faire une seule fois)
```bash
cd ~/3edges/3edges-blog

# Configurer Git pour ce repo (compte anonyme)
git config user.name "3Edges"
git config user.email "ton-email-anonyme@example.com"

# Vérifier la configuration
git config user.name
git config user.email
```

### Lier au repository GitHub
```bash
cd ~/3edges/3edges-blog

# Ajouter le remote
git remote add origin https://github.com/3edgesstrategy/3edges.github.io.git

# OU avec SSH (si configuré) :
# git remote add origin git@github.com:3edgesstrategy/3edges.github.io.git

# Vérifier
git remote -v
```

## ✍️ Workflow quotidien

### Créer un nouvel article
```bash
cd ~/3edges/3edges-blog

# Créer un article
hugo new posts/mon-nouvel-article.md

# L'article sera créé dans content/posts/ avec draft: true
```

### Tester en local
```bash
cd ~/3edges/3edges-blog

# Lancer le serveur de développement (inclut les drafts)
hugo server -D

# Ouvrir http://localhost:1313 dans le navigateur
# Le site se recharge automatiquement à chaque modification
```

### Publier un article
```bash
cd ~/3edges/3edges-blog

# 1. Éditer l'article et mettre draft: false dans le front matter

# 2. Ajouter les modifications
git add .

# 3. Commiter
git commit -m "Add new article: titre de l'article"

# 4. Pusher (déploiement automatique via GitHub Actions)
git push origin main
```

## 📝 Gestion du contenu

### Structure des fichiers
```
3edges-blog/
├── content/
│   └── posts/           # Tes articles ici
├── static/              # Images, CSS custom, etc.
├── layouts/             # Templates personnalisés
│   └── partials/
│       └── extend_head.html  # Support LaTeX
├── hugo.toml            # Configuration du site
└── .github/
    └── workflows/
        └── hugo.yml     # Déploiement automatique
```

### Ajouter des images
```bash
# 1. Copier l'image dans static/
cp ~/path/to/image.png ~/3edges/3edges-blog/static/

# 2. Référencer dans l'article
![Description](image.png)
```

### Ajouter des graphiques depuis freqtrade-docker
```bash
# Copier les graphiques de volatilité
cp ~/Documents/freqtrade-docker/python_utils/volatility_term_structure_all.png \
   ~/3edges/3edges-blog/static/

# Copier d'autres résultats
cp ~/Documents/freqtrade-docker/python_utils/*.csv \
   ~/3edges/3edges-blog/static/data/
```

## 🔧 Commandes Hugo utiles

### Générer le site (sans serveur)
```bash
cd ~/3edges/3edges-blog
hugo
# Le site est généré dans public/
```

### Lister tous les articles
```bash
cd ~/3edges/3edges-blog
hugo list all
```

### Vérifier la configuration
```bash
cd ~/3edges/3edges-blog
hugo config
```

## 🌐 Déploiement

### Première publication
```bash
cd ~/3edges/3edges-blog

# S'assurer que tout est commité
git add .
git commit -m "Initial blog setup"

# Créer la branche main et pusher
git branch -M main
git push -u origin main

# GitHub Actions va automatiquement :
# 1. Builder le site avec Hugo
# 2. Déployer sur GitHub Pages
# 3. Le site sera accessible sur https://3edges.github.io
```

### Activer GitHub Pages (sur GitHub.com)
1. Aller sur le repository : https://github.com/3edgesstrategy/3edges.github.io
2. Settings → Pages
3. Source → "GitHub Actions"
4. Attendre quelques minutes
5. Le site sera accessible sur https://3edges.github.io

### Vérifier le déploiement
```bash
# Sur GitHub.com, aller dans l'onglet "Actions"
# Tu verras le workflow "Deploy Hugo site to Pages"
# Clique dessus pour voir les logs
```

## 🐛 Dépannage

### Le site ne se déploie pas
```bash
# Vérifier le statut du workflow sur GitHub.com
# Onglet "Actions" → Voir les logs d'erreur

# Vérifier que le thème est bien présent
cd ~/3edges/3edges-blog
git submodule update --init --recursive
```

### Erreur de build Hugo
```bash
# Tester le build en local
cd ~/3edges/3edges-blog
hugo

# Si erreur, vérifier hugo.toml et les articles
```

### Les équations LaTeX ne s'affichent pas
```bash
# Vérifier que l'article a math: true dans le front matter
# Vérifier que extend_head.html existe dans layouts/partials/
```

## 📚 Ressources

- **Hugo Docs** : https://gohugo.io/documentation/
- **PaperMod Wiki** : https://github.com/adityatelange/hugo-PaperMod/wiki
- **MathJax** : https://www.mathjax.org/
- **GitHub Pages** : https://pages.github.com/

## 🎯 Checklist avant publication

- [ ] Article écrit et relu
- [ ] `draft: false` dans le front matter
- [ ] Images copiées dans `static/`
- [ ] Équations LaTeX testées en local
- [ ] Code syntax highlighting vérifié
- [ ] Tags et catégories ajoutés
- [ ] Testé avec `hugo server -D`
- [ ] Commité et pushé
- [ ] Vérifié sur https://3edges.github.io après déploiement
