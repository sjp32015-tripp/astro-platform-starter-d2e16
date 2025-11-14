# Ground Game Guidance - Website Setup Guide

## ✅ What's Already Done

Your website is built and deployed! Here's what's working:

### Home Page (`/`)
- Professional pricing display with two tiers:
  - **$29 Community Access** - Basic membership
  - **$79 Full Community Access** - Premium membership (highlighted with gold border)
- "Login Here" button for existing members
- Responsive design (mobile-friendly)
- Fixed background image setup (ready for your lion crest)

### Community Hub Page (`/community`)
- YouTube video embed system
- Grid layout for displaying multiple videos
- Instructions for adding videos
- Responsive design

### Login Page (`/login`)
- Clean login interface
- Recommendations for auth providers
- Navigation links

---

## 📋 Next Steps to Complete

### 1. Upload Your Lion Crest Background Image

**What to do:**
1. Go to your GitHub repository: https://github.com/sjp32015-tripp/astro-platform-starter-d2e16
2. Navigate to `public/images/`
3. Click "Add file" → "Upload files"
4. Upload your `GGG-FACEBOOK-IMAGE-3.jpg` file
5. Rename it to `lion-crest.jpg` (or update the path in `src/layouts/Layout.astro` line 44)
6. Commit the changes

**Result:** Your lion crest will appear as the fixed background on all pages with content scrolling over it.

---

### 2. Add Your YouTube Videos

**What to do:**
1. Open `src/pages/community.astro` in GitHub or VS Code
2. Find the `videos` array (around line 6)
3. Add your video information:

```javascript
const videos = [
  { 
    id: 'YOUR_YOUTUBE_VIDEO_ID', 
    title: 'Your Video Title', 
    description: 'Description of the video' 
  },
  { 
    id: 'ANOTHER_VIDEO_ID', 
    title: 'Second Video', 
    description: 'Another description' 
  },
  // Add more videos as needed
];
```

**How to get YouTube Video ID:**
- From URL: `https://www.youtube.com/watch?v=dQw4w9WgXcQ`
- The ID is: `dQw4w9WgXcQ` (everything after `v=`)

**Result:** Videos will automatically display in a responsive grid on the community page.

---

### 3. Set Up Stripe Payment Processing

**Current Status:** The pricing buttons link to `/.netlify/functions/create-checkout` but the Stripe function needs configuration.

**What to do:**

#### Option A: Use the Existing Stripe Function
1. Go to Netlify Dashboard → your site → Functions
2. Check if `create-checkout` function exists
3. Add your Stripe keys to Environment Variables:
   - `STRIPE_SECRET_KEY`
   - `STRIPE_PUBLISHABLE_KEY`
4. Update the function to handle the `tier` parameter (community or full)
5. Create products in Stripe dashboard for $29 and $79

#### Option B: Create New Stripe Checkout
1. Create file: `netlify/functions/create-checkout.js`
2. Add Stripe checkout code
3. Set up webhooks for payment confirmation
4. Connect to your membership system

**Stripe Dashboard:** https://dashboard.stripe.com/

---

### 4. Set Up Member Authentication

**Recommended: Netlify Identity (Easiest)**

**Steps:**
1. Go to Netlify Dashboard → your site → Identity
2. Click "Enable Identity"
3. Settings → Registration preferences → "Invite only" (or "Open" if you want anyone to sign up)
4. Settings → External providers → Enable Google, GitHub, etc. (optional)
5. Add to your site:
```html
<!-- Add to Layout.astro <head> -->
<script src="https://identity.netlify.com/v1/netlify-identity-widget.js"></script>
```

6. Update `src/pages/login.astro` to use the Netlify Identity widget
7. Protect `/community` route with authentication check

**Alternative Options:**
- **Supabase** (more features, free tier): https://supabase.com/
- **Auth0** (enterprise): https://auth0.com/
- **Clerk** (modern, good UX): https://clerk.com/

---

### 5. Add Admin Role for Video Management

**What to do:**
1. In Netlify Identity, assign yourself an admin role
2. Create an admin dashboard page: `src/pages/admin.astro`
3. Add a form to input video IDs and titles
4. Store videos in:
   - A JSON file in your repo, or
   - A database (Supabase, Firebase, etc.), or
   - Netlify CMS

**Simple approach:**
For now, you can manually edit `src/pages/community.astro` to add videos since you're the only admin.

---

### 6. Connect Payment to Membership

**What to do:**
1. Set up Stripe webhooks
2. When payment succeeds:
   - Create user account in Netlify Identity
   - Assign role based on tier (community or full)
   - Send welcome email
3. Update community page to check user role
4. Show different content based on membership tier

---

## 🛠️ File Structure

```
astro-platform-starter-d2e16/
├── src/
│   ├── layouts/
│   │   └── Layout.astro         # Main layout with background image
│   ├── pages/
│   │   ├── index.astro          # Home page with pricing
│   │   ├── community.astro      # Members-only hub with videos
│   │   └── login.astro          # Login page
│   └── components/
├── public/
│   └── images/
│       ├── corgi.jpg            # Replace with lion-crest.jpg
│       └── (your lion image)    # Upload here
└── netlify/
    └── functions/               # Serverless functions
```

---

## 💡 Quick Customization Tips

### Change Colors
Edit the style sections in each `.astro` file:
- Primary blue: `#2563eb`
- Gold accent: `#FFD700`
- Dark overlay: `rgba(0, 0, 0, 0.4)`

### Update Pricing
- Edit `src/pages/index.astro`
- Change the price numbers and features list

### Add More Pages
Create new files in `src/pages/`:
- `about.astro` → `/about`
- `contact.astro` → `/contact`
- `blog/index.astro` → `/blog`

---

## 🚀 Deployment

Netlify automatically deploys when you push to GitHub:
1. Make changes in VS Code or GitHub
2. Commit and push
3. Netlify builds and deploys (2-3 minutes)
4. Site updates at: https://groundgameguidance.com

---

## ❓ Need Help?

### Common Issues

**Site not updating?**
- Check Netlify dashboard → Deploys
- Look for build errors
- Clear browser cache

**Images not showing?**
- Check file path: `/images/lion-crest.jpg`
- Ensure image is in `public/images/`
- Try hard refresh (Ctrl+Shift+R)

**Styling looks broken?**
- Check browser console for errors
- Verify all `.astro` files have closing `</style>` tags

### Resources
- Astro Docs: https://docs.astro.build
- Netlify Docs: https://docs.netlify.com
- Stripe Docs: https://stripe.com/docs

---

## 🎯 Priority Order

1. ✅ **Upload lion crest image** (5 minutes)
2. ✅ **Add your first YouTube video** (5 minutes)
3. 🔵 **Set up Netlify Identity** (30 minutes)
4. 🔵 **Configure Stripe payments** (1 hour)
5. 🔵 **Connect payment to membership** (2 hours)
6. 🔵 **Test end-to-end flow** (30 minutes)

---

**Built with ❤️ for Steven Powers - Ground Game Guidance**