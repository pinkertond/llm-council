# Making Your LLM Council Repository Private

This guide explains how to make your fork or copy of the LLM Council repository private on GitHub.

## Why Make It Private?

You may want to make this repository private for several reasons:
- **Personal Use**: You're using this for your own research or work
- **Custom Configurations**: You've customized council members or prompts
- **Conversation History**: You want to keep your conversation data private
- **API Keys**: Extra precaution even though keys are already gitignored

## What's Already Protected

The repository is already configured to protect sensitive information:
- ✅ `.env` file (containing `OPENROUTER_API_KEY`) is gitignored
- ✅ `data/` directory (containing conversation history) is gitignored
- ✅ `node_modules/` and build artifacts are gitignored

## How to Make Your Repository Private

### If You Own This Repository

1. **Go to Repository Settings**
   - Navigate to your repository on GitHub
   - Click on **Settings** (tab in the repository navigation bar)

2. **Scroll to the Danger Zone**
   - Scroll down to the bottom of the Settings page
   - Find the section labeled **"Danger Zone"**

3. **Change Visibility**
   - Click **"Change visibility"**
   - Select **"Change to private"**
   - Confirm by typing the repository name when prompted
   - Click **"I understand, change repository visibility"**

### If You Forked This Repository

**Note**: You cannot make a fork private if the parent repository is public. You have two options:

**Option 1: Detach the Fork (Recommended)**
1. Contact GitHub Support to detach your fork (makes it an independent repository)
2. Once detached, follow the steps above to make it private

**Option 2: Create a New Private Repository**
1. Create a new **private** repository on GitHub
2. Clone your current fork locally (if not already cloned)
3. Change the remote URL to your new private repository:
   ```bash
   git remote set-url origin https://github.com/YOUR_USERNAME/NEW_REPO_NAME.git
   ```
4. Push all branches:
   ```bash
   git push -u origin --all
   git push -u origin --tags
   ```

### If You're Creating a New Copy

When creating a new repository from this template or code:
1. Click **"Use this template"** or **"Import repository"** on GitHub
2. **Uncheck** the "Public" option
3. **Check** the "Private" option
4. Complete the repository creation

## Verifying Privacy

After making your repository private:
1. Go to your repository on GitHub
2. Look for a **"Private"** badge next to the repository name
3. Try accessing the repository URL in an incognito/private browser window
4. You should see a 404 error if you're not logged in

## Additional Security Best Practices

Even with a private repository, follow these security practices:

### 1. Never Commit Secrets
```bash
# Always verify before committing
git status
git diff

# Check for accidentally staged secrets
git diff --cached
```

### 2. Use Environment Variables
All sensitive data should be in `.env` files:
```bash
# .env (already gitignored)
OPENROUTER_API_KEY=sk-or-v1-...
```

### 3. Review Your Git History
If you accidentally committed secrets in the past:
```bash
# Search for potential secrets in history
git log -p | grep -i "api.*key"

# If found, use git-filter-repo or BFG Repo-Cleaner to remove them
# Then force-push (only safe before sharing with others)
```

### 4. Limit Repository Access
If collaborating:
- Go to Settings → Collaborators
- Only add people who need access
- Use appropriate permission levels (Read, Write, Admin)

### 5. Enable Branch Protection
For collaborative work:
- Settings → Branches → Add branch protection rule
- Protect your main branch
- Require pull request reviews
- Require status checks to pass

## Sharing Your Private Repository

If you need to share with specific people:

1. **Add Collaborators**
   - Settings → Collaborators → Add people
   - Enter their GitHub username
   - They'll receive an invitation

2. **Use GitHub Teams** (for organizations)
   - Create a team in your organization
   - Add the team to your repository with appropriate permissions

## What Stays Public

Making the repository private does not affect:
- Your OpenRouter API usage (still billed to your account)
- The models you query (they still process your requests)
- Any GitHub Actions workflows (if you add them)

## Troubleshooting

**Can't find the Settings tab?**
- You must be the repository owner or have admin access

**Fork can't be made private?**
- GitHub doesn't allow private forks of public repositories
- Use Option 2 above (create a new private repository)

**Already committed secrets?**
- Rotate the compromised credentials immediately
- Remove them from git history using `git-filter-repo` or `BFG Repo-Cleaner`
- Force-push the cleaned history (if you haven't shared the repo)

## Questions?

This is a personal project by the original author. For questions about:
- **Repository privacy**: Refer to [GitHub's documentation](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/managing-repository-settings/setting-repository-visibility)
- **Security best practices**: Check [GitHub's security guides](https://docs.github.com/en/code-security)
- **The LLM Council code**: See README.md and CLAUDE.md

---

**Remember**: Making a repository private is a GitHub account/repository setting, not a code change. No modifications to the codebase are needed to make the repository private.
