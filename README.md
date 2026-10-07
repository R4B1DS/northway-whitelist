# NorthWay Whitelist System

OAuth2-based whitelist application system for the **NorthWay** GTA RP server —
originally planned under the name **NoWay RP** before the project's rebrand.

Users authenticate with Discord, submit an application form, and moderators
review it through a web panel. Approved applicants automatically receive the
whitelisted role on Discord.

> Originally developed in 2022 under the `pro1niki` account.
> Migrated to this account in 2026.
> README structure refined with AI assistance — the codebase and architecture
> are the original work.

<div align="center">

![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=node.js&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?style=for-the-badge&logo=express&logoColor=white)
![Discord.js](https://img.shields.io/badge/Discord.js-5865F2?style=for-the-badge&logo=discord&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![Sequelize](https://img.shields.io/badge/Sequelize-52B0E7?style=for-the-badge&logo=sequelize&logoColor=white)

</div>

---

## Overview

A complete whitelist pipeline for roleplay servers: authentication, application,
review, approval, and role assignment — all automated and configurable from
a single panel.

## Features

- 🔐 **Discord OAuth2 login** — no passwords stored
- 📝 **Configurable application form** — questions stored in the database
- 👨‍⚖️ **Moderator review panel** — approve, reject, or ban applicants
- 🎭 **Automatic role assignment** — approved users receive the role instantly
- 💬 **Direct message notifications** — custom approval / rejection messages
- 🔁 **Attempt limits** — configurable per-user submission cap
- 📊 **Server status integration** — live query via GameDig
- 🎨 **Branding** — custom logo and banner

## Tech Stack

| Layer | Technology |
| --- | --- |
| Runtime | Node.js |
| Backend | Express · Passport (Discord OAuth2) |
| Database | MySQL · Sequelize |
| Bot | Discord.js |
| Templates | EJS |
| Monitoring | GameDig |

## Project Structure

```
server/         Express app, routes, OAuth2 strategy
views/          EJS templates
public/         Static assets (logo, banner, CSS)
config.json     Application settings (guild, roles, database, status)
.env            Credentials and secrets — not committed
sqlsite.sql     Database schema and seed data
```

> **Note:** `config.json` and `.env` hold credentials and identifiers. Both are
> provided as templates only. Real values are never committed to this
> repository. See the **Configuration** section below.

## Database Schema

Three tables:

| Table | Purpose |
| --- | --- |
| `configs` | Global settings — logo, banner, roles, messages, attempt limit |
| `forms` | Submitted applications with status (`pending` / `approved` / `rejected`) |
| `questions` | Configurable application questions |

## Setup

**1. Clone the repository**

```bash
git clone https://github.com/R4B1DS/northway-whitelist.git
cd northway-whitelist
```

**2. Install dependencies**

```bash
npm install
```

**3. Configure environment**

Create a `.env` file at the root (a template is provided as `env.txt`) and
fill in the required values from the [Discord Developer Portal](https://discord.com/developers/applications).

The application reads all credentials and connection strings from environment
variables and from `config.json`. Refer to the template files for the exact
field names and structure.

> 🔒 **Security:** Never commit `.env` or a filled-in `config.json`. Both are
> listed in `.gitignore`. If credentials are ever leaked, rotate them
> immediately in the Discord Developer Portal and your database.

**4. Import the database**

Import `sqlsite.sql` into your MySQL instance:

```bash
mysql -u root -p < sqlsite.sql
```

**5. Run**

```bash
npm start
```

Open the local address printed in the terminal and log in with Discord.

## Configuration

The application is configured through two files, both of which are **not**
tracked in version control:

- `.env` — environment variables (authentication credentials, session secret, port)
- `config.json` — application settings (guild, roles, database connection, server status)

Template versions are provided in the repository so new installations can
copy them and fill in their own values. Refer to those templates for field
names and structure.

## Security Notes

- Discord OAuth2 — no passwords stored in the database
- Server-side session management via `express-session`
- Role-based access control for the moderator panel
- All credentials and identifiers live outside version control
- Input validation on application submission

> ⚠️ **Note:** This codebase is from 2022. The `discord.js` v12 dependency is
> deprecated. See the roadmap below for planned updates.

## Roadmap

- [ ] Upgrade `discord.js` v12 → v14
- [ ] Remove deprecated `paypal-rest-sdk` dependency
- [ ] Migrate MySQL → PostgreSQL
- [ ] Migrate Sequelize → Prisma
- [ ] Replace EJS with a modern frontend (Next.js / Astro)
- [ ] Add rate limiting per IP
- [ ] Add audit log for moderator actions
- [ ] Add unit and integration tests

## License

MIT — free to use, modify, and redistribute.

---

<div align="center">

Originally built for the **NorthWay** GTA RP community (formerly planned as **NoWay RP**).

<sub>README structure and wording refined with AI assistance. Code and architecture are original work from 2022.</sub>

</div>
