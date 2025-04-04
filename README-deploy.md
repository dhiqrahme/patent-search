# Patent Search - Free Deployment Guide

You can deploy this application to a free hosting service like Render.com without paying anything. This guide will walk you through the process.

## Step 1: Export Your Data
Run this command in your Replit terminal to export all patent data:
```bash
npx tsx scripts/export-db.ts
```
This will create JSON files with all your patents in the `exports/` directory.

## Step 2: Download Your Exported Data
1. In Replit, navigate to the "Files" panel
2. Find the `exports` folder
3. Right-click on it and select "Download"
4. Save the ZIP file to your computer

## Step 3: Set Up GitHub Repository
1. Create a free GitHub account if you don't have one (at github.com)
2. Create a new repository
3. Download your entire Replit project as a ZIP file
4. Upload the code to your GitHub repository
5. Make sure to include the exports folder with your patent data

## Step 4: Deploy to Render.com (Free Tier)
1. Create a free Render.com account at render.com
2. From your Render dashboard, create a new PostgreSQL database:
   - Choose the free plan
   - Note the "External Database URL" after creation
3. Create a new Web Service:
   - Connect your GitHub repository
   - Choose the Node runtime environment
   - Set build command: `npm install && npm run build`
   - Set start command: `NODE_ENV=production node dist/index.js`
4. Set these environment variables:
   - `DATABASE_URL`: (use the External Database URL from your Render database)
   - `SERP_API_KEY`: (your current API key)
   - `GOOGLE_PATENTS_API_KEY`: (your current API key)
   - `NODE_ENV`: production

## Step 5: Import Your Data
1. After deployment, go to the "Shell" tab in your Render web service
2. Upload your exports folder
3. Run the import script:
```bash
npm install -g tsx
npx tsx scripts/import-db.ts
```

Your application will now be running for free on Render.com! The free tier has some limitations (the application will sleep after 15 minutes of inactivity and wake up when someone visits it), but it's perfect for a project like this.

## Other Free Hosting Options
- Railway.app: Offers $5 of free credits per month
- Netlify + Supabase: For a more advanced setup with free tiers
- Vercel + PlanetScale: Another powerful free option
