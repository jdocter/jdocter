# Personal website

This repository contains a Jekyll website configured for
**https://jdocter.github.io/jdocter/**. The homepage is `index.md`.

The setup follows [GitHub's Jekyll startup guide](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll)
and uses [GitHub's Jekyll deployment workflow](https://github.com/actions/starter-workflows/blob/main/pages/jekyll-gh-pages.yml).
`README.md` remains your GitHub profile README and is excluded from the website.

## Preview locally

Use Ruby 3.3 or newer and Bundler. From the repository directory, run:

```sh
bundle install
bundle exec jekyll serve --livereload
```

Open **http://127.0.0.1:4000/jdocter/**. Save changes to `index.md` to rebuild
the preview automatically. Restart Jekyll after changing `_config.yml`.
Press Ctrl+C in the terminal to stop the server.

For a production build without starting a server:

```sh
JEKYLL_ENV=production bundle exec jekyll build
```

Jekyll generates the website in `_site/`; that directory is ignored by Git.
`Gemfile.lock` is ignored as directed by the GitHub guide. The Gemfile selects
the supported `github-pages` 232 release.

## Publish on GitHub

1. Review, commit, and push the website files to `main`:

   ```sh
   git add .gitignore Gemfile _config.yml index.md cv.md 404.md SETUP.md .github/workflows/pages.yml _layouts assets imgs/headshot.jpg
   git commit -m "Set up personal website with Jekyll and GitHub Pages"
   git push origin main
   ```

2. Open [the repository's Pages settings](https://github.com/jdocter/jdocter/settings/pages).
3. Under **Build and deployment → Source**, select **GitHub Actions**.
4. Open **Actions → Deploy Jekyll site to GitHub Pages → Run workflow** if the
   first push ran before Pages was enabled.
5. Once deployment succeeds, visit **https://jdocter.github.io/jdocter/**.

Later pushes to `main` automatically rebuild and deploy the website.

## Edit your website

- Update `index.md` to change your role, bio, publications, teaching, or the plain-text
  details in the Contact section.
- The `role` field supports Markdown links, such as `[Group name](https://example.com)`.
- For your headshot, create `assets/images/`, add `headshot.jpg`, and set
  `headshot: "/assets/images/headshot.jpg"` at the top of `index.md`.
  Until then, a labeled placeholder reserves the photo space.
- The current photo is `imgs/headshot.jpg`, exported from the JPEG preview
  embedded in `imgs/DSC09217.arw`. The original RAW file is excluded from
  the website build. The photo keeps its original landscape proportions
  without cropping. Adjust `.home-grid`'s columns in the CSS to change its width.
- The CV is not displayed on the website. `cv.md` is retained as a local
  draft and excluded from the published site.
- Update `_config.yml` to change the site title, description, or email.
- Edit `assets/css/site.css` to change colors, typography, and spacing.
- The `:root` block at the top contains the main colors, fonts, font size,
  and content width. Your name and section headings use Garamond; paper titles,
  body text, collaborators, and venues use the system sans-serif font. Section
  headings are 32px regular and paper titles are 17px semibold. Collaborators are regular and venues
  are italic. Details are indented beneath each title.
  There are no horizontal section-divider borders.
- The site uses self-hosted EB Garamond in `assets/fonts/`, with its license
  in `OFL.txt`. Adjust `.publication` margins and line height in the CSS
  to change spacing within and between publication entries.
- Edit `_layouts/default.html` to change the header, navigation, or footer.
  This custom layout replaces the default GitHub Markdown-style theme.
- Edit `_layouts/home.html` to change the arrangement of your name and photo.
  The `.home-grid` styles put the name above the bio on the left and the
  photo on the right, with publications and contact spanning the width below.
  The columns stack vertically on small screens. Bio text stays in `index.md`.
- Put images and downloadable files in an `assets/` directory. Use
  `[Download a file]({{ '/assets/document.pdf' | relative_url }})` for links to local files,
  so they include the `/jdocter` path.
- Add another page with YAML front matter, for example `about.md`:

  ```markdown
  ---
  title: About
  permalink: /about/
  ---

  # About

  Write your biography here.
  ```

  Link to it from the homepage with
  `[About]({{ '/about/' | relative_url }})`.

## Use the root address instead

For **https://jdocter.github.io/**, GitHub requires a repository named
`jdocter.github.io`. If you move the site to that repository, set these values
in `_config.yml`:

```yaml
baseurl: ""
repository: jdocter/jdocter.github.io
```

Keep `url: "https://jdocter.github.io"`. The local preview will then be at
**http://127.0.0.1:4000/**.
