<a href="https://demo-nextjs-with-supabase.vercel.app/">
  <img alt="Next.js and Supabase Starter Kit - the fastest way to build apps with Next.js and Supabase" src="https://demo-nextjs-with-supabase.vercel.app/opengraph-image.png">


  # Next.js + Supabase Starter Kit

> Le moyen le plus rapide de créer des applications avec Next.js et Supabase.

---

## Sommaire

- [Fonctionnalités](#fonctionnalités)
- [Démo](#démo)
- [Déploiement sur Vercel](#déploiement-sur-vercel)
- [Installation en local](#installation-en-local)
- [Configuration des variables d'environnement](#configuration-des-variables-denvironnement)
- [Ressources complémentaires](#ressources-complémentaires)

---

## Fonctionnalités

- Compatible avec l'ensemble de la stack **Next.js** :
  - App Router
  - Pages Router
  - Middleware
  - Composants Client & Serveur
- Authentification par mot de passe via la [Supabase UI Library](https://supabase.com/ui/docs/nextjs/password-based-auth)
- Authentification cloud via [Stack Auth](https://stack-auth.com)
- Gestion des sessions via cookies avec `supabase-ssr`
- Stylisation avec [Tailwind CSS](https://tailwindcss.com)
- Composants UI via [shadcn/ui](https://ui.shadcn.com/)
- Déploiement simplifié via l'intégration Vercel + Supabase (variables d'environnement assignées automatiquement)

---

## Démo

Une démo fonctionnelle est disponible ici : [demo-nextjs-with-supabase.vercel.app](https://demo-nextjs-with-supabase.vercel.app/)

---

## Déploiement sur Vercel

Cliquez sur le lien ci-dessous pour créer un compte Supabase, un projet, et déployer automatiquement l'application sur Vercel avec toutes les variables d'environnement configurées.

[→ Déployer sur Vercel](https://vercel.com/new/clone?repository-url=https%3A%2F%2Fgithub.com%2Fvercel%2Fnext.js%2Ftree%2Fcanary%2Fexamples%2Fwith-supabase&project-name=nextjs-with-supabase&repository-name=nextjs-with-supabase&demo-title=nextjs-with-supabase&demo-url=https%3A%2F%2Fdemo-nextjs-with-supabase.vercel.app%2F)

> Le dépôt sera également cloné sur votre GitHub, vous pourrez ensuite le cloner localement pour développer.

---

## Installation en local

### Prérequis

- Node.js 18+
- Un projet Supabase (créez-en un sur [database.new](https://database.new))

### Étapes

**1. Créer l'application depuis le template**

```bash
# npm
npx create-next-app --example with-supabase with-supabase-app

# yarn
yarn create next-app --example with-supabase with-supabase-app

# pnpm
pnpm create next-app --example with-supabase with-supabase-app
```

**2. Se placer dans le répertoire du projet**

```bash
cd with-supabase-app
```

**3. Initialiser Stack Auth**

Stack Auth gère l'authentification cloud de votre projet. Initialisez-le avec la CLI officielle :

```bash
npx @stackframe/stack-cli@latest init
```

Puis connectez votre projet à Stack Auth Cloud :

```bash
stack auth cloud
```

> Cela configure automatiquement les variables d'environnement nécessaires à Stack Auth dans votre projet.

**4. Configurer les variables d'environnement Supabase**

Renommez le fichier `.env.example` en `.env.local` :

```bash
cp .env.example .env.local
```

Puis renseignez les valeurs Supabase (voir la section [Variables d'environnement](#configuration-des-variables-denvironnement) ci-dessous).

**5. Lancer le serveur de développement**

```bash
npm run dev
```

L'application est accessible sur [http://localhost:3000](http://localhost:3000).

**6. (Optionnel) Changer le thème shadcn/ui**

Le kit utilise le style shadcn/ui par défaut. Pour en choisir un autre, supprimez `components.json` et [réinstallez shadcn/ui](https://ui.shadcn.com/docs/installation/next).

---

## Configuration des variables d'environnement

Toutes les variables se trouvent dans le fichier `.env.local` à la racine du projet.  
Les valeurs Supabase sont disponibles dans les **paramètres API** de votre projet :  
`Supabase Dashboard → Project Settings → API`

```env
# .env.local

NEXT_PUBLIC_SUPABASE_URL=https://<votre-project-ref>.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=<votre-anon-key>
```

### Détail des variables

| Variable | Visibilité | Description |
|---|---|---|
| `NEXT_PUBLIC_SUPABASE_URL` | Public (exposée côté client) | URL de votre projet Supabase. Unique par projet, elle identifie votre instance Supabase. Format : `https://<project-ref>.supabase.co` |
| `NEXT_PUBLIC_SUPABASE_ANON_KEY` | Public (exposée côté client) | Clé anonyme (JWT) permettant d'accéder à l'API Supabase avec les droits définis par les politiques RLS (Row Level Security). Sans danger à exposer côté client car les accès sont contrôlés par RLS. |

### Variables avancées (optionnelles)

Si vous avez besoin d'accès administrateur depuis le serveur uniquement (ex. : scripts de migration, webhooks), vous pouvez ajouter :


| Variable | Visibilité | Description |
|---|---|---|
| `SUPABASE_SERVICE_ROLE_KEY` | **Privé** (serveur uniquement) | Clé de service avec droits admin complets, **bypasse les politiques RLS**. À utiliser uniquement dans des contextes sécurisés (API routes serveur, fonctions serverless). Ne jamais exposer dans le navigateur. |

### Où trouver ces valeurs ?

1. Rendez-vous sur [supabase.com/dashboard](https://supabase.com/dashboard)
2. Sélectionnez votre projet
3. Allez dans **Project Settings → API**
4. Copiez :
   - **Project URL** → `NEXT_PUBLIC_SUPABASE_URL`
   - **anon / public** → `NEXT_PUBLIC_SUPABASE_ANON_KEY`
   - **service_role** → `SUPABASE_SERVICE_ROLE_KEY` *(si nécessaire)*

> **Bonne pratique :** Ne committez jamais `.env.local` dans votre dépôt Git. Le fichier est déjà ignoré par défaut via `.gitignore`.

---

## Ressources complémentaires

- [Stack Auth — Documentation](https://docs.stack-auth.com)
- [Next.js Subscription Payments Starter](https://github.com/vercel/nextjs-subscription-payments)
- [Cours gratuit : Cookie-based Auth & Next.js 13 App Router](https://youtube.com/playlist?list=PL5S4mPUpp4OtMhpnp93EFSo42iQ40XjbF)
- [Supabase Auth & Next.js App Router (exemple officiel)](https://github.com/supabase/supabase/tree/master/examples/auth/nextjs)
- [Documentation : développement local Supabase](https://supabase.com/docs/guides/getting-started/local-development)

---

## Feedback & Issues

Pour tout retour ou problème, ouvrez une issue sur le [dépôt GitHub Supabase](https://github.com/supabase/supabase/issues/new/choose). 
