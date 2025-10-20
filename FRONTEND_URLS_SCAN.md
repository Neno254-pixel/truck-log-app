# Frontend URLs Scan Report

## 🔍 All URLs Found in Frontend Code

### 1. Backend API URLs (Railway)

#### Main API Endpoint

**File:** `frontend/src/App.js` (Line 33)

```javascript
const res = await axios.post(
  "https://track-app-production-9522.up.railway.app/api/trip/",
  formData
);
```

**Purpose:** Submit trip data to create route and logs

---

#### Location Search Endpoint

**File:** `frontend/src/components/TripForm.jsx` (Line 26)

```javascript
const response = await fetch(
  `https://track-app-production-9522.up.railway.app/api/locations/search/?q=${encodeURIComponent(
    query
  )}`
);
```

**Purpose:** Autocomplete location search

---

#### PDF Download URL

**File:** `frontend/src/components/ResultPanel.jsx` (Line 56)

```javascript
<a href={`https://track-app-production-9522.up.railway.app/media/${result.pdf_url}`} target="_blank" rel="noopener noreferrer">
```

**Purpose:** Download generated PDF log sheets

---

### 2. External Service URLs

#### OpenStreetMap Tiles

**File:** `frontend/src/components/MapView.jsx`

```javascript
url = "https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png";
```

**Purpose:** Load map tiles for Leaflet map display

---

#### OpenStreetMap Attribution

**File:** `frontend/src/components/MapView.jsx`

```javascript
attribution =
  '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors';
```

**Purpose:** Map attribution link

---

#### Leaflet Marker Icons (Green)

**File:** `frontend/src/components/MapView.jsx`

```javascript
iconUrl: "https://raw.githubusercontent.com/pointhi/leaflet-color-markers/master/img/marker-icon-2x-green.png";
```

**Purpose:** Green marker icon for start location

---

#### Leaflet Marker Icons (Red)

**File:** `frontend/src/components/MapView.jsx`

```javascript
iconUrl: "https://raw.githubusercontent.com/pointhi/leaflet-color-markers/master/img/marker-icon-2x-red.png";
```

**Purpose:** Red marker icon for end location

---

#### Leaflet Marker Shadow

**File:** `frontend/src/components/MapView.jsx` (Used twice)

```javascript
shadowUrl: "https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.7.1/images/marker-shadow.png";
```

**Purpose:** Shadow image for map markers

---

### 3. Documentation URLs

#### Create React App Vitals

**File:** `frontend/src/index.js`

```javascript
// Learn more: https://bit.ly/CRA-vitals
```

**Purpose:** Documentation link (comment only)

---

#### Jest DOM Documentation

**File:** `frontend/src/setupTests.js`

```javascript
// learn more: https://github.com/testing-library/jest-dom
```

**Purpose:** Documentation link (comment only)

---

## 📊 URL Summary by Category

### Your Backend URLs (Railway) - 3 URLs

1. **API Trip Endpoint:** `https://track-app-production-9522.up.railway.app/api/trip/`
2. **Location Search:** `https://track-app-production-9522.up.railway.app/api/locations/search/`
3. **PDF Media Files:** `https://track-app-production-9522.up.railway.app/media/`

### External Services - 5 URLs

1. **OpenStreetMap Tiles:** `https://{s}.tile.openstreetmap.org/`
2. **OSM Copyright:** `https://www.openstreetmap.org/copyright`
3. **Green Marker Icon:** `https://raw.githubusercontent.com/pointhi/leaflet-color-markers/`
4. **Red Marker Icon:** `https://raw.githubusercontent.com/pointhi/leaflet-color-markers/`
5. **Marker Shadow:** `https://cdnjs.cloudflare.com/ajax/libs/leaflet/`

### Documentation Links - 2 URLs

1. **CRA Vitals:** `https://bit.ly/CRA-vitals` (comment)
2. **Jest DOM:** `https://github.com/testing-library/jest-dom` (comment)

---

## ✅ Current Configuration Status

### Backend URLs - ALL UPDATED ✓

All backend URLs are correctly pointing to your Railway deployment:

- ✅ `https://track-app-production-9522.up.railway.app`

### Frontend Deployment - CONFIGURED ✓

- ✅ Vercel URL: `https://frontend-two-ochre-86.vercel.app`
- ✅ Vercel configuration file created
- ✅ Automatic deployments enabled

### External Services - NO CHANGES NEEDED ✓

All external service URLs are standard third-party services:

- OpenStreetMap (map tiles)
- GitHub (marker icons)
- Cloudflare CDN (marker shadows)

---

## 🔒 Security Notes

### Your URLs (Configurable)

- **Railway Backend:** Can be changed in Railway dashboard
- **Vercel Frontend:** Can be changed in Vercel dashboard or add custom domain

### External URLs (Fixed)

- **OpenStreetMap:** Free public tile server
- **GitHub Raw:** Public CDN for marker icons
- **Cloudflare CDN:** Public CDN for Leaflet assets

---

## 🎯 Website Summary

### Your Production Websites:

1. **Main Frontend Application**

   - URL: https://frontend-two-ochre-86.vercel.app
   - Platform: Vercel
   - Purpose: User-facing truck log application
   - Features: Trip form, map view, log display, PDF download

2. **Backend API Service**

   - URL: https://track-app-production-9522.up.railway.app
   - Platform: Railway
   - Purpose: REST API for route calculation and log generation
   - Endpoints: `/api/trip/`, `/api/locations/search/`, `/media/`

3. **GitHub Repository**
   - URL: https://github.com/Neno254-pixel/truck-log-app
   - Purpose: Source code repository
   - Features: Version control, automatic deployments

---

**All URLs are properly configured and pointing to the correct services!**
