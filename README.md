# KrishiSahay — Team Vertex

A hackathon MVP scaffold based on the Team Vertex presentation: compare mandi options by estimated net return, explore shared transport, calculate spoilage-aware profit, record a preliminary human-reviewed visual grade, and compare sell-now/wait considerations.

## Important scope notes

- This is a runnable starter/demo, not a deployed website.
- All built-in mandi figures are hypothetical demo data. The UI explicitly labels them as **DEMO DATA — NOT LIVE**.
- The three PPT example outcomes for 4 quintals are nearby ₹4,600, distant own truck ₹4,900, and distant shared truck ₹6,300. The Profit Calculator shows these as a separate worked example.
- KisanGrade image upload currently previews the photo and records a manual preliminary grade in the UI. It does **not** claim to run a trained image model.
- Market recommendations are calculated locally from the entered figures. No AI provider, API key, or paid usage is required.
- Real market data, actual driver matching/booking, persistent harvest save/load, and production auth flow require configuration and additional integration.

## Stack mapping

- **Frontend:** Next.js / React / TypeScript / CSS; build and refine in Replit AI. Use Codium/Qodo as a coding assistant for review and tests.
- **Builder.io:** use for visual design/content editing or Builder integrations. It is not the database or the main business-logic backend.
- **Recommendations:** deterministic, browser-side explanations based on the displayed market calculations.
- **Database + Auth:** Supabase. `supabase/schema.sql` provides an initial schema and row-level security policies. Auth modal supports sign-in/sign-up when env vars are configured.
- **Debugging/observability:** use Mentalify during your debugging workflow. Highlight.io is not included in this starter; add and configure a currently supported SDK version only when you are ready to enable observability.

## Run locally / in Replit

1. Create a new Replit Node.js project or import this project.
2. Install dependencies: `npm install`
3. Copy `.env.example` to `.env.local`.
4. Add:
   - `NEXT_PUBLIC_SUPABASE_URL`
   - `NEXT_PUBLIC_SUPABASE_ANON_KEY`
5. In Supabase SQL Editor, run `supabase/schema.sql`.
6. Run `npm run dev`.

Do not expose service-role keys in the browser. Use only the Supabase anon/publishable key on the client, with RLS policies enabled. Store secret keys only in server-side environment variables.

## Deploy to GitHub Pages (no AI key required)

This version is a static Next.js export. The repository includes `.github/workflows/deploy-pages.yml`, which builds the `out/` folder and publishes it to GitHub Pages when changes are pushed to `main`.

1. Push these changes to the `main` branch.
2. In GitHub, open **Settings → Pages** and set **Source** to **GitHub Actions**.
3. Open the repository’s **Actions** tab and watch “Deploy static site to GitHub Pages” complete.
4. Open `https://shresth3.github.io/KrishiSahay_Team_Vertex_website_starter/`.

The calculator, market comparison, local explanation, photo preview, and demo pooling work without keys. Supabase sign-in is optional; add its two public environment values at build time only if you want real sign-in.

## Builder.io usage

Connect the repository to your Builder.io workflow if you use its visual editing/code generation tools. Preserve the existing calculations, auth boundaries, API validation, and demo-data labels. Do not let visual regeneration replace working logic with nonfunctional mockups. `NEXT_PUBLIC_BUILDER_API_KEY` is reserved for an optional Builder integration; it is not required to run this starter.

## Pre-demo checklist

- [ ] Add Supabase env vars and test sign-in/sign-up.
- [ ] Verify RLS in Supabase with two different test users.
- [ ] Add a trusted market-price source before claiming prices are live; display source and timestamp.
- [ ] Test negative, empty, and very large quantities/costs.
- [ ] Test the profit example: ₹4,800 − ₹200 = ₹4,600; ₹7,200 − ₹2,000 − ₹300 = ₹4,900; ₹7,200 − ₹600 − ₹300 = ₹6,300.
- [ ] Confirm image upload file type/size checks and keep grade human-reviewed.
- [ ] If observability is needed, add and configure a currently supported Highlight.io SDK version with your project ID before claiming it is active.
- [ ] Run `npm run build` and fix all errors before deployment.
