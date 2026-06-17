---
description: Initialize a new repository with essential files (LICENSE, README, .gitignore, etc.)
---

Initialize a new repository with all essential files and structure.

This workflow sets up a complete repository foundation including:
- LICENSE.md (Apache 2.0 or MIT recommended)
- README.md (with project structure)
- .gitignore (language-specific)
- CONTRIBUTING.md (optional)
- CODE_OF_CONDUCT.md (optional)
- MAINTAINERS.md (add the current Committer by default)
- Makefile (use the required minimum targets)

**Input**: Optionally specify which components to initialize. If omitted, will prompt for each.

**Steps**

1. **Assess current repository state**

   Check what already exists:
   ```bash
   ls -la LICENSE* README* .gitignore CONTRIBUTING* CODE_OF_CONDUCT* 2>/dev/null
   ```

   Identify:
   - Which files are missing
   - Which files are empty or incomplete
   - Repository type (detect from existing files/directories)

2. **Initialize LICENSE file**

   Use the **Skill tool** to invoke `init-license`:
   ```
   Invoke init-license skill to set up repository license
   ```

   This will:
   - Check for existing LICENSE files
   - Prompt user to choose license (recommend Apache 2.0 or MIT)
   - Download from official sources
   - Customize with copyright info if needed
   - Save as LICENSE.md

   **Skip if:** LICENSE file already exists and user doesn't want to replace it

3. **Create or update README.md**

   **If README.md is missing:**
   - Create basic README structure:
     ```markdown
     # Project Name
     
     Brief description of what this project does.
     
     ## Features
     
     - Feature 1
     - Feature 2
     
     ## Installation
     
     ```bash
     # Installation instructions
     ```
     
     ## Usage
     
     ```bash
     # Usage examples
     ```
     
     ## License
     
     This project is licensed under the [LICENSE_TYPE] - see the [LICENSE.md](LICENSE.md) file for details.
     
     ## Contributing
     
     Contributions are welcome! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for details.
     ```

   **If README.md exists but is minimal:**
   - Ask user if they want to enhance it with standard sections
   - Add missing sections (Installation, Usage, License, Contributing)

   **Customization:**
   - Ask user for project name and description
   - Detect project type (Python, Node.js, Go, etc.) from files
   - Add language-specific installation/usage examples
   - Link to LICENSE.md with correct license type

4. **Create .gitignore**

   **Detect project type:**
   - Check for `package.json` → Node.js
   - Check for `requirements.txt`, `setup.py`, `pyproject.toml` → Python
   - Check for `go.mod` → Go
   - Check for `Cargo.toml` → Rust
   - Check for `pom.xml`, `build.gradle` → Java
   - Check for `.csproj` → C#
   - Multiple types → Ask user which to prioritize

   **Download appropriate .gitignore template:**
   ```bash
   # For Node.js
   curl -sS https://raw.githubusercontent.com/github/gitignore/main/Node.gitignore -o .gitignore
   
   # For Python
   curl -sS https://raw.githubusercontent.com/github/gitignore/main/Python.gitignore -o .gitignore
   
   # For Go
   curl -sS https://raw.githubusercontent.com/github/gitignore/main/Go.gitignore -o .gitignore
   ```

   **If .gitignore exists:**
   - Ask if user wants to merge with standard template
   - Preserve existing entries, add missing common patterns

   **Add common entries:**
   ```
   # Editor files
   .vscode/
   .idea/
   *.swp
   *.swo
   *~
   
   # OS files
   .DS_Store
   Thumbs.db
   
   # Environment
   .env
   .env.local
   ```

5. **Create CONTRIBUTING.md (optional)**

   Ask user: "Would you like to add a CONTRIBUTING.md file?"

   **If yes:**
   - Create standard contributing guidelines:
     ```markdown
     # Contributing to [Project Name]
     
     Thank you for your interest in contributing!
     
     ## How to Contribute
     
     1. Fork the repository
     2. Create a feature branch (`git checkout -b feature/amazing-feature`)
     3. Commit your changes (`git commit -m 'Add amazing feature'`)
     4. Push to the branch (`git push origin feature/amazing-feature`)
     5. Open a Pull Request
     
     ## Development Setup
     
     [Add project-specific setup instructions]
     
     ## Code Style
     
     [Add code style guidelines]
     
     ## Testing
     
     [Add testing requirements]
     
     ## License
     
     By contributing, you agree that your contributions will be licensed under the [LICENSE_TYPE].
     ```

   - Customize with project-specific details
   - Add DCO (Developer Certificate of Origin) if needed:
     ```markdown
     ## Developer Certificate of Origin
     
     All commits must be signed off with `git commit -s` to indicate agreement with the DCO.
     ```

6. **Create CODE_OF_CONDUCT.md (optional)**

   Ask user: "Would you like to add a Code of Conduct?"

   **If yes:**
   - Recommend Contributor Covenant (industry standard)
   - Download from official source:
     ```bash
     curl -sS https://www.contributor-covenant.org/version/2/1/code_of_conduct/code_of_conduct.md -o CODE_OF_CONDUCT.md
     ```
   - Customize contact information section

7. **Initialize git repository (if needed)**

   **If not a git repository:**
   ```bash
   git init
   git add .
   git commit -m "Initial commit: Add LICENSE, README, and .gitignore"
   ```

   **If already a git repository:**
   - Ask if user wants to commit the new files
   - If yes:
     ```bash
     git add LICENSE.md README.md .gitignore CONTRIBUTING.md CODE_OF_CONDUCT.md
     git commit -m "docs: Add repository documentation and license"
     ```

8. **Display summary**

   Show what was created/updated:
   - List of files created
   - List of files updated
   - License type selected
   - Project type detected
   - Next steps (if any)

**Output On Success**

```
## Repository Initialized

**Files Created:**
✓ LICENSE.md (Apache License 2.0)
✓ README.md (with project structure)
✓ .gitignore (Python template)
✓ CONTRIBUTING.md
✓ CODE_OF_CONDUCT.md (Contributor Covenant v2.1)

**Project Type:** Python
**License:** Apache License 2.0
**Git Status:** Changes committed

**Next Steps:**
1. Update README.md with your project description
2. Add installation and usage instructions
3. Review and customize CONTRIBUTING.md for your workflow
4. Update CODE_OF_CONDUCT.md contact information

Your repository is ready for development!
```

**Output On Partial Completion**

```
## Repository Partially Initialized

**Files Created:**
✓ LICENSE.md (MIT License)
✓ README.md

**Skipped:**
- .gitignore (already exists)
- CONTRIBUTING.md (user declined)
- CODE_OF_CONDUCT.md (user declined)

**Next Steps:**
1. Review and update README.md
2. Consider adding CONTRIBUTING.md for open source projects

Repository initialization complete.
```

**Guardrails**

- Always check for existing files before creating
- Never overwrite without explicit user confirmation
- Preserve existing content when merging (e.g., .gitignore)
- Use official sources for templates (GitHub, Contributor Covenant)
- Detect project type automatically when possible
- Provide sensible defaults but allow customization
- Show clear summary of what was done
- Commit to git only if user confirms
- For LICENSE, always use the init-license skill (don't duplicate logic)
- Make all optional components truly optional - don't force them

**Project Type Detection**

| Files Present | Project Type |
|--------------|--------------|
| package.json | Node.js |
| requirements.txt, setup.py, pyproject.toml | Python |
| go.mod | Go |
| Cargo.toml | Rust |
| pom.xml, build.gradle | Java |
| *.csproj | C# |
| Gemfile | Ruby |
| composer.json | PHP |

**Template Sources**

- .gitignore: https://github.com/github/gitignore
- Code of Conduct: https://www.contributor-covenant.org/
- LICENSE: Official sources (Apache.org, GNU.org, etc.) via init-license skill

**Integration with init-license Skill**

This workflow uses the `init-license` skill for LICENSE initialization. The skill handles:
- Checking for existing licenses
- Prompting for license type (Apache 2.0 or MIT recommended)
- Downloading from official sources
- Customizing with copyright information
- Saving as LICENSE.md

The workflow focuses on orchestrating multiple initialization tasks, while delegating license-specific logic to the dedicated skill.
