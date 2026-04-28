# Chatapp Render Deployment Setup Guide

## 🚀 Complete Step-by-Step Setup

### STEP 1: Generate Required Secrets

Before you do anything, generate these secure values locally.

#### Generate JWT_SECRET:
```bash
node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
```
**Save this value** - you'll need it in Step 2.

Example output:
```
a7f3k9m2x8c1q4r5t9w2e3y4u5i6o7p8a1s2d3f4g5h6j7k8l9z0x1c2v3b4
```

---

### STEP 2: Access Render Dashboard

1. Go to: https://dashboard.render.com
2. Click on **Services** in the left sidebar
3. Click on **chatapp** service

You should see your deployment status.

---

### STEP 3: Update Environment Variables

1. In the chatapp service, click the **Environment** tab
2. You'll see all the environment variables we set with placeholders

**Update each one:**

#### 3a. JWT_SECRET
- **Key:** `JWT_SECRET`
- **Value:** Paste the secret you generated in Step 1
- Click **Save**

#### 3b. MONGO_URI (MongoDB Connection)

**Option A: Using MongoDB Atlas (Recommended - Free)**

1. Go to: https://www.mongodb.com/cloud/atlas
2. Sign up or log in
3. Create a free cluster:
   - Click "Create" button
   - Choose "Free" tier
   - Select region closest to you
   - Click "Create Cluster"

4. Get your connection string:
   - Click "Connect" button
   - Choose "Drivers"
   - Copy the connection string
   - Replace `<password>` with your database password
   - Replace `myFirstDatabase` with `chatapp`

Example format:
```
mongodb+srv://username:password@cluster0.xxxxx.mongodb.net/chatapp?retryWrites=true&w=majority
```

5. In Render dashboard:
   - **Key:** `MONGO_URI`
   - **Value:** Your MongoDB connection string
   - Click **Save**

#### 3c. CLIENT_URL

- **Key:** `CLIENT_URL`
- **Value:** `https://chatapp-wf1f.onrender.com` (your Render app URL)
- Click **Save**

#### 3d. RESEND_API_KEY (Email Service)

**Setup Resend (Free tier available):**

1. Go to: https://resend.com
2. Sign up
3. Go to API Keys section
4. Create an API key
5. Copy the key

In Render dashboard:
- **Key:** `RESEND_API_KEY`
- **Value:** Your Resend API key
- Click **Save**

#### 3e. EMAIL_FROM & EMAIL_FROM_NAME

- **Key:** `EMAIL_FROM`
- **Value:** `noreply@yourdomain.com` (or the email Resend provides)
- Click **Save**

- **Key:** `EMAIL_FROM_NAME`
- **Value:** `Chat App`
- Click **Save**

#### 3f. CLOUDINARY_* (Image Upload)

**Setup Cloudinary (Free tier available):**

1. Go to: https://cloudinary.com
2. Sign up
3. Get your credentials from dashboard:
   - Cloud Name
   - API Key
   - API Secret

In Render dashboard (update each):
- **Key:** `CLOUDINARY_CLOUD_NAME`
- **Value:** Your cloud name
- Click **Save**

- **Key:** `CLOUDINARY_API_KEY`
- **Value:** Your API key
- Click **Save**

- **Key:** `CLOUDINARY_API_SECRET`
- **Value:** Your API secret
- Click **Save**

#### 3g. ARCJET_* (Security/Rate Limiting)

**Setup Arcjet (Free tier available):**

1. Go to: https://arcjet.com
2. Sign up
3. Create a project
4. Get your API key

In Render dashboard:
- **Key:** `ARCJET_KEY`
- **Value:** Your Arcjet API key
- Click **Save**

- **Key:** `ARCJET_ENV`
- **Value:** `production`
- Click **Save**

---

### STEP 4: Monitor Deployment

After saving environment variables:

1. Click the **Logs** tab
2. Watch the build process:
   ```
   Building Docker image...
   Installing dependencies...
   npm run build
   Starting application...
   ```

3. Wait for: `Server running on port: 3000`

This means your app is live! ✅

---

### STEP 5: Test Your Application

1. Open: https://chatapp-wf1f.onrender.com
2. You should see the login page
3. Try to sign up with an email
4. You should receive a welcome email (from Resend)
5. Try logging in

---

### STEP 6: Verify Key Features

**Test these features:**

1. **Sign Up** - Create a new account
2. **Email Verification** - Check you received welcome email
3. **Profile Picture Upload** - Upload an image (uses Cloudinary)
4. **Send Messages** - Start a chat
5. **Online Status** - See who's online

---

### STEP 7: Troubleshooting

#### App won't start?
- Check **Logs** tab for errors
- Look for missing environment variables
- Verify MONGO_URI is correct

#### Emails not sending?
- Verify RESEND_API_KEY is set
- Check your email inbox/spam folder
- Verify EMAIL_FROM is correct

#### Image uploads failing?
- Verify CLOUDINARY_* keys are correct
- Check account hasn't exceeded free tier limits

#### Login issues?
- Check JWT_SECRET is set
- Verify cookies are enabled in browser
- Check browser console for errors

---

### STEP 8: Monitor in Production

**Regular checks:**

1. Go to: https://dashboard.render.com/web/srv-d7o2j2tckfvc73fbkcl0
2. Monitor:
   - **Logs** - Check for errors
   - **Metrics** - CPU, Memory usage
   - **Events** - Deployment history

---

### ✅ Checklist

- [ ] JWT_SECRET generated and set
- [ ] MongoDB Atlas cluster created and MONGO_URI set
- [ ] Resend account created and API key set
- [ ] Email addresses configured
- [ ] Cloudinary account created and keys set
- [ ] Arcjet account created and key set
- [ ] Deployment logs show "Server running"
- [ ] Test sign up works
- [ ] Test login works
- [ ] Test email sending works
- [ ] Test image upload works

---

### 📝 Service Documentation

**MongoDB Atlas:** https://docs.atlas.mongodb.com/
**Resend:** https://resend.com/docs
**Cloudinary:** https://cloudinary.com/documentation
**Arcjet:** https://docs.arcjet.com
**Render:** https://render.com/docs

---

### 🆘 Need Help?

If something doesn't work:
1. Check the **Logs** in Render dashboard
2. Verify all environment variables are set
3. Test locally first: `npm run dev`
4. Check API service status pages

Good luck! 🎉
