# Pantheon API Docs

This website is built using [Docusaurus 2](https://v2.docusaurus.io/).

## Setup

```console
npm install
npm start
```

`npm start` starts a local development server on http://localhost:3000 and opens a browser window, which will auto-reload as you make changes to the documentation.

## Deployment
We deploy to Vercel. To deploy, you only need to commit your changes and push to a branch on GitHub. You can view docs for your branch at http://pantheon-git-branchname.vercel.app. After your PR is merged to master, the updated docs should show up on http://vercel.app in about 2 minutes.

## Editing Documentation
Reference documentation for each microservice should be edited in an `openapi.yaml` file in the service's repo. Our CI pipeline will automatically build the OpenAPI spec into a Markdown file and push it to this repo, which will update the live docs.

All other forms of documentation (guides, blog posts, etc) and static pages should be edited directly here. Blog posts go into the blog/ folder, and static pages are built as React files in src/pages/. See [the Docusaurus docs](https://v2.docusaurus.io/docs/) for more details.