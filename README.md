# Kerrie Kustoms Studios Ticket Bot

A Railway-ready Discord bot and lightweight web dashboard using the requested pink, gold, and black branding.

## Included

- Private ticket channel creation from a Discord button
- Claim and close ticket controls
- Ticket counts in the dashboard and `/ticket-stats`
- Welcome and goodbye messages
- Optional automatic role assignment
- Dashboard settings for welcome messages and UI colors
- SQLite storage

## 1. Create your Discord application

1. Open the [Discord Developer Portal](https://discord.com/developers/applications).
2. Create an application named **Kerrie Kustoms Studios Ticket Bot**.
3. Open **Bot** and create/reset the bot token. Keep it private.
4. Under **Bot > Privileged Gateway Intents**, enable **Server Members Intent**.
5. Copy the **Application ID** from General Information.
6. Invite the bot using OAuth2 URL Generator. Select scopes `bot` and `applications.commands`.
7. Grant permissions: View Channels, Send Messages, Read Message History, Manage Channels, Manage Roles, and Embed Links.
8. Make sure the bot's role is above any role it should assign.

## 2. Upload this project to GitHub

1. Download and unzip this project.
2. Create a new repository on [GitHub](https://github.com/new), for example `kerrie-kustoms-ticket-bot`.
3. Upload the contents of the unzipped folder to the repository root. Make sure `package.json`, `railway.json`, and `src/` are at the top level.
4. Do **not** upload your `.env` file or bot token.

## 3. Deploy on Railway

1. Open [Railway](https://railway.app/).
2. Create a new project and choose **Deploy from GitHub repo**.
3. Select your repository.
4. In the service's **Variables** tab, add:
   - `DISCORD_TOKEN` = your bot token
   - `DISCORD_CLIENT_ID` = your Discord Application ID
   - `DASHBOARD_PASSWORD` = a long, unique password
   - `PORT` = `3000` (Railway also supplies PORT automatically)
   - `GUILD_ID` = optional test server ID; omit for global commands
5. Deploy. Railway should run `npm start`.
6. In Railway, add a **Volume** mounted at `/app/data` so SQLite data persists across redeploys.
7. Generate a public domain under **Settings > Networking**.

Your dashboard will be at the Railway domain. Use the dashboard password you set in Variables.

## 4. Configure Discord

In your server, run:
- `/ticket-panel` — posts the ticket panel in the current channel.
- `/setup-welcome channel:#welcome` — chooses the welcome channel.
- `/setup-goodbye channel:#goodbye` — chooses the goodbye channel.
- `/set-auto-role role:@Member` — sets the role automatically given to new members.
- `/ticket-stats` — shows ticket counts.

For the bot to create tickets, its role must have Manage Channels and the bot must be able to view the category/channel where the panel is posted.

## Dashboard

- Enter the `DASHBOARD_PASSWORD`.
- Select a server.
- Use Welcome to edit welcome/goodbye text and channel IDs, and the auto-role ID.
- Use Appearance to preview and save primary, accent, and background colors.

Message placeholders:
- `{user}` — mention of the new member
- `{username}` — username
- `{server}` — server name
- `{count}` — current member count

## Local Windows test

Install Node.js 20 or newer. In PowerShell, from the project folder:

```powershell
Copy-Item .env.example .env
# Edit .env and fill in the three required values.
npm install
npm start
```

Open `http://localhost:3000`.

## Important notes

- This is a starter implementation, not a clone of the Tickets.bot service.
- The dashboard currently uses password protection rather than Discord OAuth2. Do not share the dashboard password.
- Add a Railway Volume at `/app/data`; otherwise the local SQLite database may be lost when the service is replaced.
- Never commit `.env`, bot tokens, or passwords to GitHub.
