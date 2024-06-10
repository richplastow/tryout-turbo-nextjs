# Step 2: Deploy to Vercel

[^ Notes](./00-notes.md)

## Create a GitHub account

If you don't already have one, create an account at <https://github.com/signup>
and create this repository there. This will simplify deployment to Vercel.

## Create a Vercel account

If you don't already have one, create an account at <https://vercel.com/signup>
and choose the 'Hobby' plan (for free hosting).

Enter a name associated with your GitHub account, click 'Continue with GitHub',
and complete the authorisation process to link the two accounts.

## Deploy the 'docs' app on Vercel

The 'Overview' tab of your Vercel Dashboard should currently show no projects,
and you should see 'Deploy your first project'.

- Click the 'Import' button next to 'Import Project'
- Under 'Import Git Repository' click 'Import' next to 'tryout-turbo-nextjs'
- Under 'Configure Project' click 'Deploy' (see below for defaults)
- Watch the 'Deploy' run (takes about a minute)
- You'll see 'Congratulations!' and a preview of "examples/with-tailwind - docs"
- Under 'Deploy another Project from this repo', click 'Deploy' by './apps/web'
- Under 'Configure Project' click 'Deploy' (see below for defaults)
- Watch the 'Deploy' run again (maybe cached, so might be faster)
- You'll see 'Congratulations!' and a preview of "examples/with-tailwind - web"

If you click on the preview image of the "examples/with-tailwind - web" app,
you'll see that <https://tryout-turbo-nextjs-web.vercel.app/> has been deployed.

Here's the defaults that the 'Configure Project' chooses:

- Project Name: `tryout-turbo-nextjs-docs` and `tryout-turbo-nextjs-web`
- Framework Preset: `Next.js`
- Root Directory: `apps/docs` and `apps/web`
- Build Command: `cd ../.. && turbo run build --filter={/apps/docs}...`
- Output Directory: `Next.js default`
- Install Command: `npm install --prefix=../..`
- Environment Variables: (none)

The 'Overview' tab of your Vercel Dashboard should now show the 2 projects.
