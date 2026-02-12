# Nepal IPO Hub

A complete, production-ready, static website for tracking Nepal IPOs and providing investment tools. Built with zero development cost using free CDNs, GitHub, and Cloudflare Pages.

## 🚀 Features

- **Live IPO Dashboard** - Track all active IPOs with real-time status (Upcoming/Open/Closed)
- **Bulk Result Checker** - Check multiple BOID numbers at once for IPO allotment results
- **Investment Calculators** - SIP/Compounding, Profit/Loss, and Average Cost calculators
- **IPO Luck Meter** - Calculate your probability of getting IPO allotment
- **Mobile-First Design** - Fully responsive with Tailwind CSS
- **Dark Mode** - System preference detection with manual toggle
- **Zero Maintenance** - Update data by editing JSON file on GitHub (auto-rebuilds)

## 📁 Project Structure

```
/
├── index.html                  # Home + Live IPO Dashboard
├── result-checker.html         # Bulk BOID Result Checker
├── calculators.html            # All calculators in one page
├── ipo-luck.html               # Luck / Probability Meter
├── _headers                    # Security headers for Cloudflare
├── db/
│   └── ipo-data.json           # All dynamic data (edit this to update site)
└── README.md                   # This file
```

## 🛠️ Tech Stack

- **HTML5** - Pure HTML, no build step
- **Tailwind CSS** - Via CDN (mobile-first responsive design)
- **Alpine.js v3** - Via CDN (lightweight reactivity)
- **Chart.js v4** - Via CDN (for SIP calculator charts)
- **html2canvas** - Via CDN (for sharing results as images)
- **Google Fonts** - Inter font family via CDN

**No npm, no build tools, no frameworks** - just edit and deploy!

## 🏃 Local Development

### CORS Error Fix

If you see a CORS error when opening HTML files directly, you need to use a local web server. Browsers block `file://` protocol requests for security.

**Quick Solutions:**

1. **Python (Recommended - Built-in)**
   ```bash
   python -m http.server 8000
   # or
   python3 -m http.server 8000
   ```
   Then open: `http://localhost:8000`

2. **Using Included Server Script**
   ```bash
   python server.py
   # or
   python3 server.py
   ```

3. **Node.js**
   ```bash
   node server.js
   # or
   npx http-server -p 8000
   ```

4. **VS Code**
   - Install "Live Server" extension
   - Right-click `index.html` → "Open with Live Server"

**Note:** When deployed to Cloudflare Pages or GitHub Pages, CORS won't be an issue since files are served over HTTP/HTTPS.

## 📝 How to Update Data

### Method 1: Edit JSON on GitHub (Recommended)

1. Go to your GitHub repository
2. Navigate to `db/ipo-data.json`
3. Click the pencil icon to edit
4. Update the data:
   - `active_ipos`: Array of IPO objects with fields:
     - `id`: Unique identifier
     - `name`: Company name
     - `sector`: Industry sector
     - `status`: Leave blank (auto-calculated by JavaScript)
     - `units`: Total units issued
     - `price`: Issue price per unit
     - `net_worth`: Total net worth
     - `open_date`: Opening date (YYYY-MM-DD format)
     - `close_date`: Closing date (YYYY-MM-DD format)
   - `news_ticker`: String with latest news/updates
   - `results`: Object mapping BOID numbers to allotment results
     ```json
     {
       "12345678901234": {
         "company": "Company Name",
         "kitta": 10
       }
     }
     ```
5. Commit changes (Cloudflare Pages will auto-rebuild)

### Method 2: Local Edit

1. Edit `db/ipo-data.json` locally
2. Commit and push to GitHub
3. Cloudflare Pages will automatically rebuild

## 🚢 Deployment

### Cloudflare Pages (Recommended - Free)

1. **Connect Repository**
   - Go to [Cloudflare Dashboard](https://dash.cloudflare.com)
   - Navigate to Pages → Create a project
   - Connect your GitHub repository

2. **Build Settings**
   - **Framework preset**: None
   - **Build command**: (leave empty)
   - **Build output directory**: `/` (root)
   - **Root directory**: `/` (root)

3. **Deploy**
   - Cloudflare will automatically deploy on every push to main branch
   - Custom domain can be added in Pages settings

### GitHub Pages (Alternative - Free)

1. Go to repository Settings → Pages
2. Source: Deploy from a branch
3. Branch: `main` (or `master`)
4. Folder: `/` (root)
5. Save

**Note**: GitHub Pages doesn't support `_headers` file. For security headers, use Cloudflare Pages.

## 🔒 Security

The `_headers` file includes:
- **CSP** (Content Security Policy) - Restricts resource loading
- **X-Frame-Options: DENY** - Prevents clickjacking
- **HSTS** - Forces HTTPS
- **X-Content-Type-Options: nosniff** - Prevents MIME sniffing

These headers are automatically applied by Cloudflare Pages.

## 📱 Mobile Optimization

- **Mobile-first design** - Base styles for mobile, `sm:`, `md:`, `lg:` breakpoints for larger screens
- **Touch-friendly** - Large buttons, adequate spacing
- **Responsive tables** - Horizontal scroll on mobile
- **Hamburger menu** - Collapsible navigation on mobile
- **Optimized images** - No heavy assets, fast loading

## 🎨 Customization

### Colors
Edit Tailwind classes in HTML files. Current color scheme:
- Primary: Blue (`blue-600`, `blue-400`)
- Success: Green (`green-600`, `green-400`)
- Warning: Yellow (`yellow-600`, `yellow-400`)
- Danger: Red (`red-600`, `red-400`)

### Fonts
Currently using Inter from Google Fonts. To change:
1. Update Google Fonts link in `<head>` of each HTML file
2. Update `fontFamily` in Tailwind config

### Ad Placeholders
Replace ad placeholders with actual ad code:
- `<!-- AdSense Leaderboard 728x90 -->` - Above IPO grid
- `<!-- Adsterra Sidebar 300x250 -->` - Desktop sidebar
- `<!-- Adsterra Social Bar -->` - Below form buttons
- `<!-- AdSense Vignette -->` - Between calculator sections
- `<!-- AdSense In-Article -->` - Below luck meter

## 🐛 Troubleshooting

### Data not updating?
- Check JSON syntax (use JSON validator)
- Verify file path is `./db/ipo-data.json` (relative)
- Check browser console for fetch errors
- Ensure Cloudflare Pages rebuild completed

### Dark mode not working?
- Clear browser localStorage
- Check if `darkMode` class is applied to `<html>` tag
- Verify Alpine.js is loaded (check console)

### Charts not showing?
- Verify Chart.js CDN is loaded
- Check browser console for errors
- Ensure canvas element exists before Chart.js initialization

### Mobile menu not working?
- Verify Alpine.js is loaded
- Check for JavaScript errors in console
- Ensure `x-data` and `x-show` directives are correct

## 📊 Data Format Reference

### IPO Object
```json
{
  "id": "unique-id",
  "name": "Company Name Limited",
  "sector": "Banking",
  "status": "",
  "units": 10000000,
  "price": 100,
  "net_worth": 1000000000,
  "open_date": "2024-01-15",
  "close_date": "2024-01-25"
}
```

### Results Object
```json
{
  "12345678901234": {
    "company": "Company Name Limited",
    "kitta": 10
  }
}
```

## 🎯 Best Practices

1. **Always validate JSON** before committing
2. **Use consistent date format** (YYYY-MM-DD)
3. **Keep BOID numbers as strings** in JSON (14 digits)
4. **Test locally** before pushing to production
5. **Monitor Cloudflare Pages** build logs for errors

## 📄 License

Free to use and modify. No attribution required.

## 🤝 Support

For issues or questions:
1. Check this README
2. Review browser console for errors
3. Validate JSON syntax
4. Check Cloudflare Pages build logs

## ✨ Features Checklist

- [x] Mobile-friendly responsive design
- [x] Low-maintenance JSON updates
- [x] Secure with _headers
- [x] Zero-cost stack
- [x] User-friendly/easy UI
- [x] Ad placeholders included
- [x] All features implemented
- [x] Beautiful/unique/trusted/professional UI
- [x] Dark mode working
- [x] All fetch calls relative & error-handled
- [x] Calculators give correct math
- [x] Share image feature works

---

**Built with ❤️ for Nepal investors**

