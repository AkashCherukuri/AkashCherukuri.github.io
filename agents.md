# AI Agents Guide - Akash Cherukuri's GitHub Page

This document provides context and instructions for AI agents working on this repository.

## Project Overview
This website uses [Jekyll](https://jekyllrb.com/) and is primarily based on the [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/) theme. It is hosted on GitHub Pages.

## Configuration & Architecture
- **Base Theme**: The directory structure (`_layouts`, `_includes`, `_sass`) and `_config.yml` heavily utilize `minimal-mistakes-jekyll`.
- **Hybrid State**: 
    - The `Gemfile` references a local gemspec (`minimal-mistakes-jekyll.gemspec`) AND `gem "jekyll-theme-cayman"`.
    - `_config.yml` ends with `theme: jekyll-theme-cayman`.
    - **Analysis**: The user (Akash) added the Cayman theme setting in 2021 while learning. The site structure implies Minimal Mistakes is the intended or actual functional core, while the Cayman setting might be overriding styles or ignored depending on the build context. **Agents should assume Minimal Mistakes is the primary architecture unless instructed otherwise.**

## Setup & Running Locally
**Prerequisites**:
- Ruby 3.3+ (Installed via `winget install RubyInstallerTeam.RubyWithDevKit.3.3`)
- Bundler

**Instructions**:
1.  **Install Dependencies**:
    ```bash
    bundle install
    ```

2.  **Update Dependencies (Critical for Ruby 3.x)**:
    The `Gemfile.lock` may reference older Jekyll versions incompatible with Ruby 3. Run this to upgrade to Jekyll 4.x:
    ```bash
    bundle update
    ```

3.  **Run Development Server**:
    ```bash
    bundle exec jekyll serve
    ```
    - access the site at `http://localhost:4000`.
    - **Note**: If you see `bundle : The term 'bundle' is not recognized` or `bundler: command not found: jekyll`:
        1.  Restart your terminal (to load the new PATH).
        2.  Or use the full path:
            ```powershell
            C:\Ruby33-x64\bin\bundle.bat exec jekyll serve
            ```

## Verification Notes
- **Jekyll Version**: The site runs successfully with **Jekyll 4.4.1**.
- **Build Warnings**: There is a known conflict warning:
    > `Conflict: The following destination is shared by multiple files.`
    > `_site/index.html` (from `index.html` and `_pages/index.md`)
    - This is non-fatal but implies a redundancy in the content structure.
- **Theme**: While `jekyll-theme-cayman` is in `_config.yml` and `Gemfile`, the visual structure relies on **Minimal Mistakes**. The `cayman` theme might be a legacy setting.

## Key Files
- `_config.yml`: Main configuration. Ends with `theme: jekyll-theme-cayman` (conflicts with Minimal Mistakes structure).
- `Gemfile`: References `minimal-mistakes-jekyll.gemspec` and `jekyll-theme-cayman`.
- `_pages/`: Contains content pages.
- `assets/`: Images and CSS.

## Contribution Workflow
- **Branching**: Always create a new feature branch for changes (e.g., `git checkout -b feature/name`).
- **Commits**: Make granular commits for each distinct feature or fix.
- **Verification**: ALWAYS ask the user to verify changes (by running the site locally) **before** pushing/committing to the remote.
- **Persistence**: Update this document (`agents.md`) if workflow usage changes.
