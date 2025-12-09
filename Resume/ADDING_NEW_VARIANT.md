# SOP: Adding a New Resume Variant

This document provides step-by-step instructions for adding new resume variants (e.g., for different roles like SoftwareEngineering, DataScience, ProductManagement, etc.) to the automated build and release system.

## Overview

The resume system supports multiple variants, each with:
- Independent LaTeX source files
- Separate version tracking
- Automated compilation and releases
- Role-specific release tags (e.g., `softwareengineering-v0.0.1`)

## Directory Structure

```
Resume/
├── Generic/
│   ├── Resume.tex
│   └── VERSION.txt
├── SoftwareEngineering/
│   ├── Resume.tex
│   └── VERSION.txt
├── DataScience/          # Example new variant
│   ├── Resume.tex
│   └── VERSION.txt
└── ADDING_NEW_VARIANT.md (this file)
```

## Step-by-Step Guide

### Step 1: Create the Variant Directory

```bash
cd Resume
mkdir <RoleName>  # e.g., mkdir DataScience
```

**Important:** Use PascalCase for directory names (e.g., `SoftwareEngineering`, `DataScience`, `ProductManagement`)

### Step 2: Create the LaTeX File

Copy an existing resume variant as a starting point:

```bash
cp Generic/Resume.tex <RoleName>/Resume.tex
```

Edit `<RoleName>/Resume.tex` to customize for the target role:
- Tailor experience descriptions to highlight role-relevant work
- Emphasize skills and technologies specific to the role
- Adjust projects to showcase role-appropriate expertise
- Modify sections as needed

### Step 3: Create the Version File

Initialize the version tracking:

```bash
echo "0.0.1" > <RoleName>/VERSION.txt
```

### Step 4: Commit and Push

```bash
git add Resume/<RoleName>/
git commit -m "Add <RoleName> resume variant"
git push origin main
```

### Step 5: Verify Automated Build

The GitHub Action will automatically:
1. Detect the new variant
2. Compile `<RoleName>/Resume.tex` to PDF
3. Increment version to v0.0.1
4. Create a release with tag `<rolename>-v0.0.1` (lowercase)
5. Upload `RohanBatra-<RoleName>.pdf` to the release

Check:
- GitHub Actions tab for successful workflow run
- Releases page for new tagged release
- README.md for updated version line

## How the System Works

### Change Detection
The workflow detects which `Resume/*/` directories have changed files and only builds those variants.

### Version Incrementing
Each variant has independent versioning:
- Patch version increments on each change (0.0.1 → 0.0.2)
- Rolls over at .9 (0.0.9 → 0.1.0)
- Minor rolls over at .10 (0.9.x → 1.0.0)

### Release Naming
- **Tag:** `<rolename>-v0.0.1` (lowercase variant name)
- **Title:** `<RoleName> Resume Release v0.0.1`
- **PDF:** `RohanBatra-<RoleName>.pdf`
- **Notes:** `Release of <RoleName> resume version v0.0.1`

## Updating Existing Variants

To update an existing variant:

```bash
# Edit the resume
vim Resume/<CompanyName>/Resume.tex

# Commit and push
git add Resume/<CompanyName>/Resume.tex
git commit -m "Update <CompanyName> resume: <description>"
git push origin main
```

The workflow will:
- Detect changes in that variant only
- Compile only that PDF
- Increment only that variant's version
- Create a new release for that variant

## Troubleshooting

### PDF Not Generated
- Check LaTeX syntax errors in GitHub Actions logs
- Ensure `Resume.tex` is directly in the variant directory
- Verify the file is named exactly `Resume.tex`

### Version Not Incrementing
- Ensure `VERSION.txt` exists and contains valid version (e.g., `0.0.1`)
- Check file permissions in the repository

### No Release Created
- Verify GitHub Actions has `contents: write` permissions
- Check `GITHUB_TOKEN` is available in workflow
- Ensure no duplicate tags exist

### Multiple Variants Releasing When Only One Changed
- Check that your commit only modified files in one variant directory
- Review git diff to confirm changed files

## Best Practices

1. **Keep Generic Updated:** Update `Resume/Generic/` as your baseline, then copy changes to other variants
2. **Meaningful Commits:** Use descriptive commit messages for easier tracking
3. **Test Locally:** Compile LaTeX locally before pushing to catch errors early
4. **Version Strategy:** Let the system auto-increment; don't manually edit VERSION.txt
5. **Naming Convention:** Always use PascalCase for variant directory names

## Local Compilation

To test a variant locally:

```bash
cd Resume/<CompanyName>
pdflatex Resume.tex
pdflatex Resume.tex  # Run twice for references
open Resume.pdf
```

## FAQ

**Q: Can I have more than 2-3 variants?**
A: Yes, the system supports unlimited variants. Each gets independent versioning and releases.

**Q: What if I want to update multiple variants at once?**
A: Commit changes to multiple variant directories. The workflow will build and release each one separately.

**Q: How do I delete a variant?**
A: Remove the directory and commit. Past releases remain available.

**Q: Can I customize the PDF naming?**
A: Yes, edit `.github/workflows/ci.yml` and modify the "Rename PDF for release" step.

**Q: How do I see all version history?**
A: Check the Releases page or look at `README.md` for current versions.

## Support

For issues or questions:
1. Check GitHub Actions logs for detailed error messages
2. Review this SOP for proper setup steps
3. Verify your LaTeX syntax is correct
4. Open an issue in the repository if needed

---

**Last Updated:** December 2025
**Maintainer:** Rohan Batra
