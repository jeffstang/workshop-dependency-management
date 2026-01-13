# Deployment Guide: QMD Slide Deck Rendering

## Overview

This repository is configured to automatically render and deploy the Quarto slide deck using GitHub Actions and GitHub Pages.

## How It Works

### Automatic Deployment (GitHub Actions → GitHub Pages)

1. **Trigger**: Whenever code is pushed to the `main` branch
2. **Render**: GitHub Actions runs Quarto to convert `slides/index.qmd` to HTML (RevealJS format)
3. **Deploy**: The rendered HTML is automatically deployed to GitHub Pages
4. **Access**: The slides are available at: https://jeffstang.github.io/workshop-dependency-management/

### Workflow Details

The `.github/workflows/render-slides.yml` workflow does the following:

1. **Render Job**:
   - Checks out the repository
   - Sets up Quarto
   - Renders the slides to the `docs/` directory
   - Uploads the rendered slides as both:
     - A build artifact (for download/debugging)
     - A GitHub Pages artifact

2. **Deploy Job**:
   - Deploys the rendered HTML to GitHub Pages
   - Runs only after the render job succeeds

## Setup Requirements

### GitHub Repository Settings

To enable GitHub Pages deployment, ensure the following setting is configured:

1. Go to your repository **Settings** → **Pages**
2. Under "Build and deployment":
   - **Source**: Select "GitHub Actions"
3. Save the changes

**Note**: This setting is required for the workflow to deploy successfully.

## Usage

### For Workshop Attendees

Simply visit: **https://jeffstang.github.io/workshop-dependency-management/**

The slides are always up-to-date with the latest changes from the `main` branch.

### For Local Development

If you want to preview changes before pushing:

```bash
# Install Quarto (if not already installed)
# https://quarto.org/docs/get-started/

# Render the slides locally
quarto render slides/index.qmd --to revealjs --output-dir docs

# Open in browser
open docs/index.html  # macOS
xdg-open docs/index.html  # Linux
start docs/index.html  # Windows
```

### For Contributors

1. Make changes to `slides/index.qmd`
2. (Optional) Test locally with `quarto render`
3. Commit and push to a feature branch
4. Create a pull request to `main`
5. Once merged, GitHub Actions will automatically render and deploy the updated slides

## Troubleshooting

### Slides Not Updating

If the slides don't update after merging to `main`:

1. Check the [Actions tab](https://github.com/jeffstang/workshop-dependency-management/actions) for workflow runs
2. Look for any failed workflows and check the logs
3. Verify GitHub Pages is enabled in Settings → Pages

### Workflow Fails

Common issues:

- **Permission errors**: Ensure the repository has Pages enabled with "GitHub Actions" as the source
- **Quarto render errors**: Check the "Render slides" step logs for syntax errors in the QMD file
- **Deployment errors**: Verify that the workflow has proper permissions (defined in the YAML)

### Local Rendering Issues

If `quarto render` fails locally:

- Ensure Quarto is installed: `quarto --version`
- Check for syntax errors in `slides/index.qmd`
- Verify all referenced images/files exist in the `slides/` directory

## Architecture Benefits

This setup provides several advantages:

1. **No Manual Rendering**: Slides are automatically rendered on every push to `main`
2. **Always Up-to-Date**: The published slides always reflect the latest content
3. **Preview Before Merge**: You can test changes locally before publishing
4. **Version Control**: All slide history is tracked in Git
5. **No Build Artifacts in Repo**: The `docs/` directory doesn't need to be committed
6. **Artifact Downloads**: Build artifacts are available for 90 days for debugging

## Additional Resources

- [Quarto Documentation](https://quarto.org/)
- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [RevealJS Format Options](https://quarto.org/docs/presentations/revealjs/)
