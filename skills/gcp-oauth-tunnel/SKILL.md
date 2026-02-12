---
name: gcp-oauth-tunnel
description: Set up SSH tunnels for OAuth flows on headless GCP instances. Use when (1) User pastes an OAuth URL with localhost redirect (e.g., http://127.0.0.1:PORT/oauth2/callback), (2) User is doing Google OAuth on a remote GCP server and needs browser authentication, (3) User mentions OAuth, GCP instance, and browser/port in the same request, (4) CLI tool shows "Opening browser for authorization" but server has no browser.
---

# GCP OAuth Tunnel

Automatically creates SSH tunnels to enable OAuth flows on headless GCP instances.

## How It Works

When authenticating with Google (or other OAuth providers) on a headless server:
1. CLI generates an OAuth URL with `redirect_uri=http://127.0.0.1:PORT/oauth2/callback`
2. This skill creates an SSH tunnel for that specific PORT
3. User opens the URL locally, Google redirects back through the tunnel
4. Server receives the auth code and completes authentication

## Usage

### When User Pastes an OAuth URL

Extract the port from the URL and create the tunnel:

```bash
# URL format: redirect_uri=http%3A%2F%2F127.0.0.1%3A**PORT**%2Foauth2%2Fcallback
# Example: port 37991

gcloud compute ssh INSTANCE_NAME --zone=ZONE -- -L PORT:127.0.0.1:PORT -N -f
```

Verify the tunnel:
```bash
lsof -i :PORT
```

### Port Extraction from URL

The port appears after `127.0.0.1%3A` (URL-encoded `:`):
- `http%3A%2F%2F127.0.0.1%3A**37991**%2Foauth2%2Fcallback` → Port is **37991**

### Full Workflow

1. **Identify instance details** (from context or ask user):
   - Instance name (e.g., `openclaw-gateway`)
   - Zone (e.g., `us-central1-a`)

2. **Extract port** from OAuth URL

3. **Kill existing tunnels** on that port (optional but recommended):
   ```bash
   pkill -f "ssh.*:PORT" 2>/dev/null || true
   ```

4. **Create tunnel**:
   ```bash
   gcloud compute ssh INSTANCE_NAME --zone=ZONE -- -L PORT:127.0.0.1:PORT -N -f
   ```

5. **Verify** tunnel is listening:
   ```bash
   lsof -i :PORT
   ```

6. **Instruct user** to open the OAuth URL in their local browser

## Example Interaction

**User:** "Here's my OAuth URL: https://accounts.google.com/o/oauth2/auth?...redirect_uri=http%3A%2F%2F127.0.0.1%3A**37991**%2Foauth2%2Fcallback..."

**Action:**
```bash
gcloud compute ssh openclaw-gateway --zone=us-central1-a -- -L 37991:127.0.0.1:37991 -N -f
```

**Response:** "✅ Tunnel created for port 37991. Open the URL in your browser now!"

## Troubleshooting

### Port already in use
```bash
# Find and kill existing process
lsof -i :PORT
kill -9 <PID>
```

### Tunnel not working
- Verify instance name and zone
- Check that `gcloud` is authenticated: `gcloud auth list`
- Ensure the GCP instance is running: `gcloud compute instances list`

### OAuth fails after tunnel
- The OAuth app may be in "Testing" mode - user needs to be added as a test user in Google Cloud Console
- Or the app hasn't completed Google verification - look for "Advanced" → "Continue" on error page

## User Configurations

### openclaw-gateway (us-central1-a)
```bash
gcloud compute ssh openclaw-gateway --zone=us-central1-a -- -L PORT:127.0.0.1:PORT -N -f
```

## Notes

- The port changes each time the OAuth flow is initiated
- Tunnels persist until manually killed or system restart
- To stop a tunnel: `pkill -f "ssh.*:PORT"`
