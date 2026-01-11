# Deployment Instructions

## Option 1: GitHub Pages (Recommended - Free & Easy)

1. Push your code to GitHub:
   ```bash
   git push origin main
   ```

2. Go to: https://github.com/Real-Sam/her-birthday/settings/pages

3. Under "Source", select "main" branch and "/" (root) folder

4. Click "Save"

5. Your site will be live at: **https://real-sam.github.io/her-birthday/**

---

## Option 2: Cloudflare Tunnel (Advanced)

### Prerequisites:
- Install Cloudflare Tunnel: https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/install-and-setup/

### Steps:

1. **Install cloudflared:**
   ```powershell
   # Download from: https://github.com/cloudflare/cloudflared/releases
   # Or use winget:
   winget install cloudflare.cloudflared
   ```

2. **Login to Cloudflare:**
   ```bash
   cloudflared tunnel login
   ```

3. **Create a tunnel:**
   ```bash
   cloudflared tunnel create birthday-fatima
   ```

4. **Create config file** at `C:\Users\<username>\.cloudflared\config.yml`:
   ```yaml
   tunnel: <TUNNEL-ID>
   credentials-file: C:\Users\<username>\.cloudflared\<TUNNEL-ID>.json

   ingress:
     - hostname: birthday.yourdomain.com
       service: http://localhost:8000
     - service: http_status:404
   ```

5. **Start a local server** (in your project directory):
   ```powershell
   python -m http.server 8000
   ```

6. **Run the tunnel:**
   ```bash
   cloudflared tunnel run birthday-fatima
   ```

7. **Configure DNS** in Cloudflare dashboard:
   - Add CNAME record: `birthday` -> `<TUNNEL-ID>.cfargotunnel.com`

---

## Option 3: Quick Local Share with Cloudflare Tunnel (No Domain)

1. **Install cloudflared** (if not already)

2. **Start local server:**
   ```powershell
   cd d:\birthdaycode\her-birthday
   python -m http.server 8000
   ```

3. **In another terminal, run:**
   ```bash
   cloudflared tunnel --url http://localhost:8000
   ```

4. **Copy the generated URL** (like: https://random-name.trycloudflare.com)

5. **Share the link!** (It's temporary and will expire when you close the tunnel)

---

## Option 4: Netlify Drop (Easiest for quick share)

1. Go to: https://app.netlify.com/drop

2. Drag and drop your entire `her-birthday` folder

3. Get instant live link!

---

## Recommended: GitHub Pages
**Your link will be:** https://real-sam.github.io/her-birthday/

It's free, permanent, and automatically updates when you push changes!
