# ⚠️ SECURITY CHECKLIST - READ BEFORE PUSHING TO GITHUB

## 🔴 CRITICAL SECURITY ISSUES FOUND

Your project contains **EXPOSED CREDENTIALS** that must NOT be pushed to GitHub!

### Exposed Credentials Found:

1. **MongoDB Connection String** (in both .env files):
   ```
   MONGODB_URI=mongodb+srv://ifa-hiring:pSmdw6aTJzSG22VZ@ifa-cluster...
   ```
   - Username: `ifa-hiring`
   - Password: `pSmdw6aTJzSG22VZ` ❌ EXPOSED!

2. **Google OAuth Client ID** (in both .env files):
   ```
   VITE_GOOGLE_CLIENT_ID=415852681005-l0e7c4khn5qp2lcenouasl3kkbn9v58l.apps.googleusercontent.com
   ```

## ✅ STEPS TO FIX BEFORE PUSHING

### 1. Environment Files Are Now Protected
✅ Added `.env` to `.gitignore` files
✅ Created `.gitignore` in all project folders

### 2. Initialize Git Repository Correctly
Your git repo is currently tracking files from your entire Desktop. Fix this:

```bash
# Navigate to your project
cd /Users/ajinkya/Desktop/SkillQuest

# Remove the incorrect git repository
rm -rf .git

# Initialize git correctly in the SkillQuest folder
git init

# Add files (now .env files will be ignored)
git add .

# Commit
git commit -m "Initial commit - credentials secured"
```

### 3. Verify .env Files Are Not Tracked

```bash
git status
```

You should NOT see:
- `skillquest-backend/.env`
- `SkillQuest-mongodb-oauth/.env`

If you see them, run:
```bash
git rm --cached skillquest-backend/.env
git rm --cached SkillQuest-mongodb-oauth/.env
```

### 4. Create .env.example Files

Create safe template files for other developers:

**skillquest-backend/.env.example**:
```env
MONGODB_URI=your_mongodb_connection_string_here
VITE_GOOGLE_CLIENT_ID=your_google_client_id_here
PORT=5000
FRONTEND_URL=http://localhost:5173
NODE_ENV=development
VITE_OPENAI_API_KEY=your_openai_api_key_here
```

**SkillQuest-mongodb-oauth/.env.example**:
```env
VITE_GOOGLE_CLIENT_ID=your_google_client_id_here
VITE_API_URL=http://localhost:5000/api
MONGODB_URI=your_mongodb_connection_string_here
PORT=5000
FRONTEND_URL=http://localhost:5173
NODE_ENV=development
```

### 5. Before Pushing to GitHub

Run this final check:
```bash
# Ensure .env files are ignored
git status | grep .env

# If .env files appear, DO NOT PUSH!
```

### 6. After Push - Rotate Credentials

⚠️ **IMPORTANT**: Since these credentials may have been exposed:

1. **Change MongoDB Password**:
   - Go to MongoDB Atlas
   - Database Access → Edit User
   - Change password for `ifa-hiring` user

2. **Rotate Google OAuth Client**:
   - Google Cloud Console
   - APIs & Services → Credentials
   - Create new OAuth 2.0 Client ID
   - Update your .env files

## 📝 README Section to Add

Add this to your README.md:

```markdown
## Environment Variables

This project requires environment variables. Create `.env` files in the following locations:

### Backend (.env in skillquest-backend/)
```env
MONGODB_URI=your_mongodb_uri
VITE_GOOGLE_CLIENT_ID=your_google_client_id
PORT=5000
FRONTEND_URL=http://localhost:5173
```

### Frontend (.env in SkillQuest-mongodb-oauth/)
```env
VITE_GOOGLE_CLIENT_ID=your_google_client_id
VITE_API_URL=http://localhost:5000/api
```

**Never commit .env files to version control!**
```

## 🚨 If You Already Pushed

If credentials are already on GitHub:
1. Immediately rotate all credentials
2. Use BFG Repo-Cleaner to remove from git history
3. Or delete and recreate the repository

## ✅ You're Safe to Push When:

- [ ] `.env` files are in `.gitignore`
- [ ] Git repository is initialized correctly in `/SkillQuest` folder only
- [ ] `git status` shows no `.env` files
- [ ] `.env.example` files created (optional but recommended)
- [ ] Verified no credentials in committed files

---

**Created:** 2024
**Last Updated:** Check before every push
