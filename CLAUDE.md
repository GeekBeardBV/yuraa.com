# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a personal blog site (yuraa.com) built with Jekyll using the Chirpy theme. The site is deployed to GitHub Pages via GitHub Actions workflow.

- **Site URL**: https://yuraa.com
- **Theme**: jekyll-theme-chirpy v7.4+
- **Ruby Version**: 3.3
- **Timezone**: Europe/Amsterdam
- **Theme Mode**: Dark

## Development Commands

### Local Development

Start the local development server:
```bash
bundle exec jekyll s -l
# Or use the helper script:
bash tools/run.sh
```

For production mode locally:
```bash
bash tools/run.sh -p
```

Custom host binding:
```bash
bash tools/run.sh -H 0.0.0.0
```

### Build and Test

Build the site for production:
```bash
JEKYLL_ENV=production bundle exec jekyll b -d "_site"
```

Build and run HTML proofer tests:
```bash
bash tools/test.sh
```

Or manually:
```bash
bundle exec jekyll b -d "_site"
bundle exec htmlproofer _site \
  --disable-external \
  --ignore-urls "/^http:\/\/127.0.0.1/,/^http:\/\/0.0.0.0/,/^http:\/\/localhost/"
```

### Dependency Management

Install dependencies:
```bash
bundle install
```

## Project Structure

### Key Directories

- `_posts/`: Blog posts in markdown format (currently empty, no posts yet)
- `_tabs/`: Special pages (About, Archives, Categories, Tags)
- `_data/`: Data files for contact info and sharing options
- `_plugins/`: Custom Jekyll plugins (posts-lastmod-hook.rb)
- `assets/`: Static assets (CSS, JS, images)
- `tools/`: Helper scripts for running and testing the site

### Configuration

Main site configuration is in `_config.yml`:
- Site title, tagline, description configured
- GitHub username: geekbeard
- Email: ya@yuraa.com
- PWA enabled with offline cache
- Pagination set to 10 posts per page

### Custom Plugins

- `_plugins/posts-lastmod-hook.rb`: Automatically manages post last modified dates

## Deployment

Deployment happens automatically via GitHub Actions on push to main/master branch.

Workflow file: `.github/workflows/pages-deploy.yml`

The workflow:
1. Sets up Ruby 3.3 with bundler cache
2. Builds the site with Jekyll
3. Tests with htmlproofer
4. Deploys to GitHub Pages

## DevContainer Support

A DevContainer configuration is available for VSCode:
- Based on `mcr.microsoft.com/devcontainers/jekyll:2-bullseye`
- Includes extensions for Liquid, Shell, and Markdown
- Runs post-create setup for shell enhancements

## Content Guidelines

### Creating Posts

Posts should be placed in `_posts/` with filename format: `YYYY-MM-DD-title.md`

Front matter defaults (from _config.yml):
- Layout: post
- Comments: enabled
- TOC: enabled
- Permalink: /posts/:title/

### Available Pages

The site includes these tab pages:
- About (`_tabs/about.md`)
- Archives (`_tabs/archives.md`)
- Categories (`_tabs/categories.md`)
- Tags (`_tabs/tags.md`)

## Docker Deployment

Per user instructions, home projects should be deployed to Docker containers with:
- Docker Compose files (use `docker compose` without dash)
- GitHub Actions workflow for self-hosted runner (labeled: gbsrv)
