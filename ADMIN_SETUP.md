# How to Add Admin Role in Firestore

## Step-by-Step Guide

### Step 1: Get Your User ID

First, you need to get your Firebase Auth User ID. There are two ways:

**Option A: From Firebase Console**
1. Go to [Firebase Console](https://console.firebase.google.com)
2. Select your project: **driving-209f3**
3. Click **Authentication** in the left sidebar
4. Click **Users** tab
5. You'll see a list of users with their **User UID**
6. Copy the UID of the user you want to make admin

**Option B: From Browser Console (after signing in to your app)**
1. Run your app: `npm run dev`
2. Sign in to your app
3. Open browser DevTools (F12)
4. Go to **Console** tab
5. Type: `firebase.auth().currentUser.uid`
6. Press Enter
7. Copy the UID that appears

---

### Step 2: Add Admin Role in Firestore

1. **Go to Firestore Database**
   - In Firebase Console, click **Firestore Database** in the left sidebar
   - You should see your database (if not created, click "Create database")

2. **Navigate to user_roles Collection**
   - Click **Start collection** (if this is your first collection)
   - Collection ID: `user_roles`
   - Click **Next**

3. **Add Admin Role Document**
   - **Document ID**: `{YOUR_USER_ID}_admin`
     - Replace `{YOUR_USER_ID}` with the UID you copied
     - Example: `eBMXY74LbhMJp4Bu9EV7e5UCSQS2_admin`
   
   - **Add Fields**:
     - Field 1:
       - Field name: `userId`
       - Type: `string`
       - Value: `{YOUR_USER_ID}` (same UID, without `_admin`)
     
     - Field 2:
       - Field name: `role`
       - Type: `string`
       - Value: `admin`
     
     - Field 3:
       - Field name: `createdAt`
       - Type: `timestamp`
       - Value: Click "Set to current time"

4. **Save the Document**
   - Click **Save**

---

### Step 3: Verify Admin Access

1. **Refresh Your App**
   - Go back to your running app
   - Refresh the page (F5)
   - You should now see the **Admin Dashboard** instead of Student Portal

2. **Check Admin Features**
   - You should see:
     - "Admin Dashboard" header
     - "Create Session" button
     - "Manage Students" button
     - Ability to delete sessions

---

## Quick Reference

### Document Structure
```
Collection: user_roles
Document ID: {userId}_admin

Fields:
{
  "userId": "eBMXY74LbhMJp4Bu9EV7e5UCSQS2",
  "role": "admin",
  "createdAt": Timestamp(2025-11-27 14:23:00)
}
```

### Important Notes

> [!IMPORTANT]
> - The Document ID **must** follow the pattern: `{userId}_admin`
> - The `userId` field value should match your Firebase Auth User UID exactly
> - The `role` field must be exactly `"admin"` (lowercase)

> [!TIP]
> **To add a student role** (though this is done automatically on signup):
> - Document ID: `{userId}_student`
> - role: `"student"`

> [!WARNING]
> **Security**: Only add admin roles to trusted users. Admins can:
> - Create and delete sessions
> - Manage all user roles
> - View all bookings

---

## Troubleshooting

**"Permission denied" error after adding role:**
- Make sure you refreshed the app
- Check that the Document ID matches the pattern exactly
- Verify the userId field matches your Auth UID

**Still seeing Student Dashboard:**
- Log out and log back in
- Clear browser cache
- Check Firestore rules are deployed (they are ✅)

**Can't find your User UID:**
- Sign up for a new account in your app
- Check Firebase Console → Authentication → Users
- The UID will be listed there
