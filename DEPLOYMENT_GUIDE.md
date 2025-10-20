# Deployment Guide - Truck Log App

This guide will help you deploy the Truck Log App with Railway (backend) and Vercel (frontend).

## Prerequisites

- GitHub account
- Railway account (https://railway.app)
- Vercel account (https://vercel.com)
- Git installed
- Railway CLI installed
- Vercel CLI installed (optional)

## Backend Deployment (Railway)

### Option 1: Using Railway CLI (Recommended)

1. **Navigate to backend directory:**

   ```bash
   cd backend
   ```

2. **Login to Railway:**

   ```bash
   railway login
   ```

3. **Link to existing project or create new:**

   ```bash
   railway link
   # OR create new project
   railway init
   ```

4. **Deploy:**

   ```bash
   railway up
   ```

5. **Get your Railway URL:**

   ```bash
   railway domain
   ```

   Your backend will be available at: `https://your-app.up.railway.app`

### Option 2: Using Railway Dashboard

1. Go to https://railway.app
2. Click "New Project"
3. Select "Deploy from GitHub repo"
4. Choose your `truck-log-app` repository
5. Select the `backend` directory as root
6. Railway will auto-detect Django and deploy
7. Add a domain in the Settings tab

### Environment Variables (Railway)

Set these in Railway dashboard or via CLI:

```bash
SECRET_KEY=your-secret-key-here
DEBUG=False
ALLOWED_HOSTS=.railway.app,.vercel.app
```

## Frontend Deployment (Vercel)

### Option 1: Using Vercel Dashboard (Recommended)

1. Go to https://vercel.com
2. Click "Add New Project"
3. Import your GitHub repository: `truck-log-app`
4. Configure project:
   - **Framework Preset:** Create React App
   - **Root Directory:** `frontend`
   - **Build Command:** `npm run build`
   - **Output Directory:** `build`
5. Click "Deploy"

Your frontend will be available at: `https://your-app.vercel.app`

### Option 2: Using Vercel CLI

1. **Navigate to frontend directory:**

   ```bash
   cd frontend
   ```

2. **Login to Vercel:**

   ```bash
   vercel login
   ```

3. **Deploy:**

   ```bash
   vercel --prod
   ```

4. Follow the prompts:
   - Set up and deploy? **Y**
   - Which scope? Select your account
   - Link to existing project? **N** (for new project)
   - Project name? **truck-log-app** (or custom name)
   - Directory? Press **ENTER** (uses ./)

## Post-Deployment Configuration

### Update Backend URL in Frontend

After deploying to Railway, you need to update the frontend to use your new Railway URL:

1. **Get your Railway URL:**

   ```bash
   cd backend
   railway domain
   ```

2. **Update frontend files** with your Railway URL:

   - `frontend/src/App.js` (line 33)
   - `frontend/src/components/TripForm.jsx` (line 26)
   - `frontend/src/components/ResultPanel.jsx` (line 56)

3. **Commit and push changes:**

   ```bash
   git add .
   git commit -m "Update Railway backend URL"
   git push origin master
   ```

4. **Redeploy frontend:**
   - Vercel will automatically redeploy on push
   - Or manually trigger deployment in Vercel dashboard

### Update CORS Settings in Backend

Update `backend/trucklog/settings.py` to include your Vercel URL:

```python
CORS_ALLOWED_ORIGINS = [
    "http://localhost:3000",
    "https://your-app.vercel.app",  # Add your Vercel URL
]
```

Commit and push, Railway will auto-deploy.

## Current Deployment URLs

- **Backend (Railway):** https://track-app-production-9522.up.railway.app
- **Frontend (Vercel):** To be deployed
- **GitHub Repository:** https://github.com/Neno254-pixel/truck-log-app

## Verification

### Test Backend API:

```bash
curl https://your-railway-url.up.railway.app/api/trip/ \
  -X POST \
  -H "Content-Type: application/json" \
  -d '{
    "current_location": "New York, NY",
    "pickup_location": "Philadelphia, PA",
    "dropoff_location": "Boston, MA",
    "current_cycle_hours": 5
  }'
```

### Test Frontend:

1. Open your Vercel URL in browser
2. Fill in the trip form
3. Click "Generate Route & Logs"
4. Verify map displays and logs are generated
5. Test PDF download

## Troubleshooting

### Backend Issues:

- **500 Error:** Check Railway logs: `railway logs`
- **CORS Error:** Verify CORS_ALLOWED_ORIGINS includes your Vercel URL
- **Database Error:** Railway provides PostgreSQL automatically

### Frontend Issues:

- **API Connection Failed:** Verify Railway URL is correct in frontend code
- **Build Failed:** Check Vercel build logs in dashboard
- **Blank Page:** Check browser console for errors

## Continuous Deployment

Both Railway and Vercel support automatic deployments:

- **Railway:** Auto-deploys on push to `master` branch (backend changes)
- **Vercel:** Auto-deploys on push to `master` branch (frontend changes)

## Custom Domains (Optional)

### Railway:

1. Go to Railway dashboard
2. Select your project
3. Settings → Domains
4. Add custom domain and configure DNS

### Vercel:

1. Go to Vercel dashboard
2. Select your project
3. Settings → Domains
4. Add custom domain and configure DNS

## Support

For issues:

- Check Railway logs: `railway logs`
- Check Vercel logs in dashboard
- Review GitHub repository: https://github.com/Neno254-pixel/truck-log-app

---

**Last Updated:** 2025
**Repository:** https://github.com/Neno254-pixel/truck-log-app
