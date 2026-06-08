# Keep-alive Render (toutes les 13 min)

Évite que ton app Render (free tier) s’endorme après **15 min** d’inactivité.

## Option recommandée : GitHub Actions (gratuit)

### 1. Créer le dépôt GitHub

```bash
cd "/home/kapelo/soutenance/job render"
git init
git add .
git commit -m "Add Render keep-alive cron (13 min)"
git branch -M main
git remote add origin git@github.com:kapelo-dev/soutenance_cron_job.git
git push -u origin main
```

### 2. Configurer le secret

1. GitHub → ton repo → **Settings** → **Secrets and variables** → **Actions**
2. **New repository secret**
3. Nom : `RENDER_APP_URL`
4. Valeur : `https://pdvconnect-67i4.onrender.com`

### 3. Activer les workflows planifiés

- **Actions** → workflow **Keep Render awake** → **Enable workflow**
- Test manuel : **Run workflow**

Le job tourne automatiquement toutes les **13 minutes**.

> Les crons GitHub peuvent avoir 1–5 min de retard ; 13 min reste sous la limite de 15 min Render.

---

## Option 2 : cron-job.org (sans GitHub)

1. Compte sur [cron-job.org](https://cron-job.org)
2. **Create cronjob**
   - **URL** : `https://ton-app.onrender.com`
   - **Schedule** : Custom → `*/13 * * * *` (toutes les 13 min)
3. Sauvegarder

---

## Option 3 : Render Cron Job (plan payant uniquement)

Les [Cron Jobs Render](https://render.com/docs/cronjobs) ne sont **pas** disponibles sur le free tier. Si tu passes en payant :

- **Type** : Cron Job
- **Schedule** : `*/13 * * * *`
- **Command** : `curl -fsS "$RENDER_APP_URL"`

---

## Rappel free tier Render

- ~**750 h/mois** d’instance — un service 24/7 consomme tout le quota.
- Pour économiser, limite les pings aux heures utiles (ex. 8h–20h).
