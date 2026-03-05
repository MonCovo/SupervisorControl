# Supervisor Controls Widget

A JavaScript widget that lets supervisors change voice flow global variables from their WxCC agent desktop. Based on the **Supervisor - Voice Flow changes from Desktop** concept (Cisco *From Features to Solutions*, p52+).

## Design

Uses **Momentum Design** (Cisco Webex design system) for layout and styling: cards, toggles, buttons, and typography aligned with Webex Contact Center.

## GitHub Pages Deployment

1. **Push this repo to GitHub.**

2. **Enable GitHub Pages:**
   - Repo → **Settings** → **Pages**
   - Under "Build and deployment", set **Source** to **Deploy from a branch**
   - Branch: **main** (or your default branch), Folder: **/ (root)**
   - Save

3. The site will be available at:
   - `https://<username>.github.io/<repo-name>/`

4. **For WxCC Desktop embedding:**  
   Use the full URL in the Desktop layout, e.g.  
   `https://<username>.github.io/<repo-name>/`

## Configuration

When embedding in the WxCC Desktop, assign **STORE values** in the Desktop Layout JSON so the widget receives real-time data. No token service is required.

### Desktop Layout JSON (recommended – uses signed-in user's token)

In your Desktop layout JSON, configure the widget with STORE references:

```json
{
  "access-token": "$STORE.auth.accessToken",
  "org-id": "$STORE.agent.orgId",
  "user-id": "$STORE.agent.agentId"
}
```

| Attribute       | STORE reference                | Description                          |
|-----------------|--------------------------------|--------------------------------------|
| `access-token`  | `$STORE.auth.accessToken`      | Signed-in user's bearer token        |
| `org-id`        | `$STORE.agent.orgId`           | WxCC organization ID                 |
| `user-id`       | `$STORE.agent.agentId`         | Optional: filter variables by agent  |
| `user`          | (prefix string)                | Alternative: filter by variable name prefix |

### Fallback: Token service (standalone / demo)

For use outside the Desktop (e.g. demo or standalone page), you can use a token service:

| Attribute      | Description                                      |
|----------------|--------------------------------------------------|
| `trigger-url`  | URL that returns `{ token: "..." }`              |
| `pass-phrase`  | Passphrase for the token endpoint                |

## Local Development

Serve the project with a local server, for example:

```bash
npx serve .
# or
python -m http.server 8000
```

Then open `http://localhost:8000` (or `http://localhost:8000/` for `serve`).

## Files

- `index.html` – Main page for GitHub Pages
- `app/script.js` – Supervisor controls widget (Web Component)
- `app/supervisor.html` – Minimal standalone demo page
