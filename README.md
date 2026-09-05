# SRK Super Power - Staff Face Attendance System

## Overview

A complete face recognition attendance system with local storage, geolocation verification, and Google Sheets integration.

## Features

✅ **Face Recognition** - Uses face-api.js for accurate face detection  
✅ **Staff Registration** - Create staff profiles with face capture  
✅ **Face Login/Logout** - Automated attendance with face recognition  
✅ **Geolocation Verification** - Confirm office location before logging  
✅ **Local Storage** - All data saved locally (no server needed)  
✅ **Google Sheets Sync** - Export attendance to Google Sheets  
✅ **Dashboard** - Real-time attendance statistics  
✅ **Search & Filter** - Find staff quickly  
✅ **Responsive Design** - Works on desktop and mobile  

## Quick Start

### 1. Open the Application
```bash
# Clone repository
git clone https://github.com/sandipofficial732-max/srk-super-power-apk.git
cd srk-super-power-apk

# Open index.html
open index.html  # macOS
xdg-open index.html  # Linux
start index.html  # Windows
```

### 2. Or Use a Local Server
```bash
# Python 3
python3 -m http.server 8000

# Node.js
npx http-server
```
Then open `http://localhost:8000`

## Default Login

- **Admin ID**: `admin`
- **Password**: `admin123`

**⚠️ Change these credentials before production use!**

## How to Use

### 1. Dashboard
- View daily attendance statistics
- Search for specific staff members
- See who's checked in/out
- Delete attendance records

### 2. Staff ID Creation
1. Enter Staff ID (e.g., SRK-001)
2. Enter Staff Name
3. Select Department
4. Click "Open Camera & Capture Face"
5. Look at camera and capture
6. Face is registered automatically

### 3. Face Login/Logout
1. Click "Start Camera"
2. Allow location permission
3. Face will be verified automatically
4. Click "FACE LOGIN" to clock in
5. Click "FACE LOGOUT" to clock out
6. System confirms within 2 seconds

## Requirements

- ✅ Modern browser (Chrome, Firefox, Safari, Edge)
- ✅ Camera access
- ✅ Location permission
- ✅ Internet (for first model load)

## Technical Details

### Face Recognition
- **Library**: face-api.js v0.22.2
- **Model**: TinyFaceDetector (lightweight)
- **Accuracy Threshold**: 0.48 (configurable)
- **Detection Speed**: ~1-2 seconds per frame

### Geolocation
- **Office Location**: Primarc Tower, Salt Lake, Sector V, Kolkata
- **Latitude**: 22.57617
- **Longitude**: 88.43195
- **Radius**: 180 meters

### Local Storage
- **Key**: `srk_super_power_v1`
- **Data Structure**:
  ```javascript
  {
    "staff": [{id, name, dept, mobile, descriptor}],
    "attendance": [{staffId, name, date, login, logout}]
  }
  ```

## Google Sheets Integration

### Setup
1. Create Google Apps Script Web App
2. Copy the Web App URL
3. Click "Save to Google Sheets" button
4. Paste URL when prompted
5. URL is saved for future syncs

### Sample Google Apps Script
```javascript
function doPost(e) {
  const sheet = SpreadsheetApp.getActiveSheet();
  const data = JSON.parse(e.postData.contents);
  
  // Process attendance data
  data.attendance.forEach(record => {
    sheet.appendRow([record.staffId, record.name, record.date, record.login, record.logout]);
  });
  
  return ContentService.createTextOutput('OK');
}
```

## Troubleshooting

### Camera Not Working
1. Check browser permissions (Allow camera)
2. Try incognito/private mode
3. Use HTTPS or localhost
4. Restart browser

### Face Not Detected
1. Improve lighting conditions
2. Face should be 30cm-60cm from camera
3. Clear eyeglasses if possible
4. Ensure face is fully visible

### Location Not Verified
1. Enable location services on device
2. Allow location permission
3. Move to office area (180m radius)
4. Check GPS accuracy

### Face Not Recognized
1. Ensure good lighting during registration
2. Re-capture face with better lighting
3. Different camera angles or expressions
4. Adjust threshold in code (line with dist>0.48)

## Security Notes

⚠️ **This is a demonstration system**

- Default credentials are visible
- Passwords not encrypted
- Local storage not secure
- For production:
  - Use secure authentication
  - Implement backend verification
  - Use HTTPS only
  - Add encryption
  - Implement access control

## Browser Compatibility

| Browser | Support | Notes |
|---------|---------|-------|
| Chrome | ✅ Full | Recommended |
| Firefox | ✅ Full | Works well |
| Safari | ✅ Full | iOS 14+ |
| Edge | ✅ Full | Same as Chrome |
| IE 11 | ❌ No | Not supported |

## Mobile Access

### For HTTPS Testing (Required for Mobile)

**Option 1: ngrok**
```bash
ngrok http 8000
# Opens: https://xxxx-xxxx.ngrok.io
```

**Option 2: GitHub Pages**
1. Push to GitHub repo
2. Enable Pages in Settings
3. Access via https://username.github.io/repo

**Option 3: Netlify/Vercel**
- Drag-drop folder for instant HTTPS URL

## Performance

- First load: ~5-10 seconds (model download)
- Face detection: ~1-2 seconds
- Subsequent loads: ~1 second
- Storage: ~100KB per 100 staff members

## Future Enhancements

- 📱 Mobile app (React Native)
- 🎙️ Voice confirmation
- 📊 Advanced reporting
- 👥 Team management
- 🔔 Notifications
- 📈 Analytics dashboard
- 🌙 Dark mode
- 🌍 Multi-language

## License

MIT License - Use freely for any purpose

## Support

For issues or suggestions, create an issue on GitHub.

---

**Made with ❤️ by Your Team**
