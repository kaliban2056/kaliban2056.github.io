# Hello visitor!

Welcome to my corner of the internet, journey with me through the realms of tech, security, and programming innovation. This blog is focused on sharing insights into my projects, cybersecurity, penetration testing, and privacy-related topics.

## About the Blog

This blog is powered by Hugo, a fast and flexible static site generator. The content is deployed automatically using GitHub Actions.
Features

-   Tech Projects: In-depth walkthroughs of various projects, highlighting programming and architecture decisions.
-   Cybersecurity: Insights into penetration testing, vulnerability assessments, and the latest trends in security.
-   Privacy: Discussions on the importance of data privacy, encryption, and how to stay secure online.

# Getting Started

## Prerequisites

Before working with this blog, make sure you have the following installed:

-   Hugo
-   Git
-   Go (optional, if building Hugo from source)

### Clone the Repository

```bash

git clone https://github.com/<your-username>/<your-blog-repo>.git
cd <your-blog-repo>
```

### Install Hugo (if not installed)

Follow the official Hugo installation guide based on your OS.

### Create a New Post

To add a new post to the blog:

```bash

hugo new posts/your-post-title.md
```

This command will create a new markdown file in the content/posts/ directory. Open the file, edit the front matter (metadata at the top of the file), and start writing your post in markdown format.

### Local Development

To serve the website locally and view your changes:

```bash

hugo server
```

-   Open your browser and go to: http://localhost:1313
-   Any changes you make will automatically refresh the site.

### Build the Static Website

To build the static files for deployment, run:

```bash

hugo
```

The static files will be generated in the public/ directory. These files are what GitHub Pages will use to serve your blog.

### Deploying with GitHub Actions

This blog uses GitHub Actions to automate the deployment process. Once changes are pushed to the main branch, the site is automatically built and deployed.

### GitHub Pages Setup

Make sure to enable GitHub Pages in your repository:

-   Go to your repository's settings.
-   In the Pages section, set the Source to the gh-pages branch (this is the branch where GitHub Actions will deploy the website).

### GitHub Actions Workflow

The deployment process is automated using a GitHub Actions workflow, typically located in .github/workflows/gh-pages.yml.

Here’s an example of a simple Hugo deployment workflow:

```yaml
name: Deploy Hugo Blog

on:
    push:
        branches:
            - main # Deploy only when changes are pushed to the main branch

jobs:
    build-deploy:
        runs-on: ubuntu-latest
        steps:
            - name: Checkout code
              uses: actions/checkout@v2

            - name: Setup Hugo
              uses: peaceiris/actions-hugo@v2
              with:
                  hugo-version: "latest"

            - name: Build
              run: hugo --minify

            - name: Deploy to GitHub Pages
              uses: peaceiris/actions-gh-pages@v3
              with:
                  github_token: ${{ secrets.GITHUB_TOKEN }}
                  publish_dir: ./public
```

You can also look at my `deploy.yml` in `.github/workflows`.

NOTE: Never share sensitive data such as github tokens in the GitHub actions workflow, you can read more [here](https://docs.github.com/en/actions/security-for-github-actions/security-guides/using-secrets-in-github-actions).

# Contributions

Feel free to fork the repository and submit pull requests if you'd like to contribute or improve the blog.

# License

This blog's code is open-sourced under the MIT License.
