# Troubleshooting Guide - Frontend-Backend Communication

## Issue: Frontend Not Communicating with Backend

### Quick Checklist

1. **✅ Backend URL is correct in frontend code**

   - Location: `frontend/src/App.js` line 33
   - URL: `https://track-app-production-9522.up.railway.app/api/trip/`

2. **✅ Backend API is working**

   - Tested with curl - SUCCESS
   - Returns complete data

3. **⚠️ Frontend needs redeployment**
   - Changes made to code need to be deployed to Vercel
   - Currently deploying...

---

## Common Issues & Solutions

### 1. CORS Error

**Symptom:** Browser console shows "Access-Control-Allow-Origin" error

**Solution:**
The backend already has `CORS_ALLOW_ALL_ORIGINS = True` which should allow all domains.

If you still see CORS errors, add the Vercel URL explicitly:

```python
# In backend/trucklog/settings.py
CORS_ALLOWED_ORIGINS = [
    "https://frontend-two-ochre-86.vercel.app",
    # ... other origins
]
```

### 2. Vercel Deployment Not Updated

**Symptom:** Form submits but nothing happens

**Solution:**
The frontend code changes need to be deployed to Vercel. This is currently in progress.

**Manual Redeployment:**

```bash
cd frontend
vercel --prod
```

### 3. Network Error

**Symptom:** "Failed to fetch" or "Network request failed"

**Check:**

1. Open browser Developer Tools (F12)
2. Go to Network tab
3. Submit the form
4. Look for the request to Railway backend
5. Check the response

### 4. Backend Not Responding

**Symptom:** Request times out or returns 500 error

**Test Backend Directly:**

```bash
curl -X POST https://track-app-production-9522.up.railway.app/api/trip/ \
  -H "Content-Type: application/json" \
  -d '{
    "current_location": "New York, NY",
    "pickup_location": "Philadelphia, PA",
    "dropoff_location": "Boston, MA",
    "current_cycle_hours": 5,
    "use_sleeper_berth": false
  }'
```

If this works, the backend is fine and the issue is with the frontend.

---

## Step-by-Step Debugging

### Step 1: Check Browser Console

1. Open your frontend: https://frontend-two-ochre-86.vercel.app
2. Press F12 to open Developer Tools
3. Go to "Console" tab
4. Fill in the form and submit
5. Look for any red error messages

**Common Errors:**

- `CORS policy` → CORS issue
- `Failed to fetch` → Network issue
- `404 Not Found` → Wrong URL
- `500 Internal Server Error` → Backend issue

### Step 2: Check Network Tab

1. In Developer Tools, go to "Network" tab
2. Submit the form
3. Look for a request to `track-app-production-9522.up.railway.app`
4. Click on it to see details

**What to check:**

- **Status Code:** Should be 200
- **Response:** Should contain route data
- **Headers:** Check if CORS headers are present

### Step 3: Verify Frontend Code

Check that the frontend has the correct backend URL:

```javascript
// In frontend/src/App.js line 33
const res = await axios.post(
  "https://track-app-production-9522.up.railway.app/api/trip/",
  formData
);
```

### Step 4: Check Vercel Deployment

1. Go to https://vercel.com/dashboard
2. Find your project
3. Check the latest deployment
4. Verify it's using the updated code

---

## Testing the Connection

### Test 1: Direct Backend Test

```bash
curl -X POST https://track-app-production-9522.up.railway.app/api/trip/ \
  -H "Content-Type: application/json" \
  -d @test-trip.json
```

**Expected:** JSON response with route data

### Test 2: Frontend Test

1. Visit: https://frontend-two-ochre-86.vercel.app
2. Enter:
   - Current Location: New York, NY
   - Pickup Location: Philadelphia, PA
   - Dropoff Location: Boston, MA
   - Current Cycle Hours: 5
3. Click Submit

**Expected:**

- Map displays route
- Log entries appear
- PDF download link shows

---

## If Nothing Works

### Option 1: Redeploy Frontend

```bash
cd frontend
git add .
git commit -m "Force redeploy"
git push origin master
```

Vercel will automatically redeploy.

### Option 2: Check Railway Backend

1. Go to https://railway.app/dashboard
2. Find your project
3. Check logs for errors
4. Verify the backend is running

### Option 3: Add Vercel URL to CORS

Edit `backend/trucklog/settings.py`:

```python
CORS_ALLOWED_ORIGINS = [
    "http://localhost:3000",
    "https://frontend-two-ochre-86.vercel.app",  # Add this
]
```

Then commit and push:

```bash
git add .
git commit -m "Add Vercel URL to CORS"
git push origin master
```

---

## Current Status

### ✅ Working

- Backend API (Railway)
- Backend CORS settings
- Frontend code (updated with correct URL)

### ⚠️ In Progress

- Vercel deployment (redeploying with updated code)

### 🔍 To Verify

- Frontend can reach backend
- Form submission works
- Map displays
- Logs generate

---

## Contact Information

**Backend URL:** https://track-app-production-9522.up.railway.app  
**Frontend URL:** https://frontend-two-ochre-86.vercel.app  
**GitHub:** https://github.com/Neno254-pixel/truck-log-app

---

## Quick Fix Commands

### Redeploy Frontend

```bash
cd frontend
vercel --prod
```

### Test Backend

```bash
curl -X POST https://track-app-production-9522.up.railway.app/api/trip/ \
  -H "Content-Type: application/json" \
  -d '{"current_location":"New York, NY","pickup_location":"Philadelphia, PA","dropoff_location":"Boston, MA","current_cycle_hours":5,"use_sleeper_berth":false}'
```

### Check Logs

- **Vercel:** https://vercel.com/dashboard → Your Project → Logs
- **Railway:** https://railway.app/dashboard → Your Project → Logs

---

**Last Updated:** January 2025  
**Status:** Vercel redeployment in progress
