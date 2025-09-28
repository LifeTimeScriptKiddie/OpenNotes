## 1. Understand the Core Issue

- **Obsidian Digital Garden** often makes its own commits/pushes directly to the GitHub repository behind the scenes.  
- If you make local commits in parallel without pulling those remote commits first, you can end up with diverging branches.  

**Result:** You get merge conflicts, non-fast-forward errors, or forced pushes.

---

## 2. Recommended Workflow

1. **Start by Pulling**  
   - **Anytime** you open your Obsidian vault on a machine, do a quick:
     ```bash
     git pull --rebase
     ```
     or  
     ```bash
     git pull
     ```
   - This ensures you have the latest changes, including what the Digital Garden plugin might have pushed from another device.

2. **Work on Your Notes**  
   - Add new notes, modify existing ones, etc.

3. **Obsidian Digital Garden Publishes**  
   - If you trigger a publish from Obsidian, it may create new commits in the remote repository.

4. **Pull Again Before Your Final Commit**  
   - Right before you commit and push your local changes, pull again:
     ```bash
     git pull --rebase
     ```
   - This step incorporates any commits the Digital Garden plugin made while you were working.

5. **Commit & Push Your Local Changes**  
   - Stage and commit your changes:
     ```bash
     git add .
     git commit -m "My local changes"
     ```
   - Push them:
     ```bash
     git push
     ```
   - Now your local repository and the remote are fully in sync.

6. **Repeat on Every Machine**  
   - Whenever you switch machines, just repeat the same sequence (pull first, work, publish from Obsidian, pull again if needed, then commit and push).

---

## 3. (Optional) Use a Dedicated “Publish” Branch

Some users prefer to keep Digital Garden commits isolated on a different branch (e.g., `publish` or `gh-pages`). If the plugin supports that:

1. **Configure Digital Garden** to push to `publish` (or `gh-pages`).  
2. **Work on `main`** locally, commit your notes.  
3. **When ready to publish**:  
   - Merge or rebase your `main` branch into `publish`, or just let the plugin do its own push to that branch.  
4. **Result**: The plugin’s automated commits don’t interfere with your main workflow.  

This is more advanced, and not all Obsidian publishing plugins handle a separate branch easily. If it’s supported, it can help keep your main branch clean.

---

## 4. Practical Tips & Tricks

1. **Enable “Pull Rebase by Default”**  
   If you prefer a linear history (no merge commits), set:
   ```bash
   git config --global pull.rebase true
   ```
   Then `git pull` will always rebase automatically.

2. **Watch for Merge Conflicts**  
   If you see conflict markers (`<<<<<<< HEAD`, `=======`, `>>>>>>>`), you need to decide how to merge the changes. Commit or stash your local work before pulling to reduce the risk of conflicts.

3. **Avoid Force Pushes**  
   Only force push if you really need to overwrite the remote history. In a multi-device or multi-collaborator scenario, force pushes can cause confusion for others.

4. **Use `.gitignore`**  
   Sometimes, Obsidian workspace files (`.obsidian/workspace.json`) change frequently. If you don’t care about preserving that state across machines, add it to `.gitignore` so it doesn’t cause frequent “unnecessary” commits.


---

## Mermaid Diagram

```mermaid
flowchart LR
    A[Pull official main] --> B[Work on main]
    B --> C[Commit and push to main]
    C --> D[Checkout publish branch]
    D --> E[Pull rebase from publish]
    E --> F[Merge or rebase main into publish]
    F --> G[Resolve conflicts and commit]
    G --> H[Push publish]
    H --> I[Digital Garden plugin]
    I --> J[Site published from publish]
```

1. **Pull official main** – Update your local `main` from the remote repo.  
2. **Work on main** – Make edits in Obsidian.  
3. **Commit and push** – Send changes to `origin/main`.  
4. **Checkout publish** – Switch to the `publish` branch.  
5. **Pull rebase from publish** – Get the latest changes on the `publish` branch.  
6. **Merge or rebase** – Bring `main` changes into `publish`.  
7. **Resolve conflicts** – If needed, fix and commit.  
8. **Push publish** – Update the remote `publish` branch.  
9. **Digital Garden plugin** – Detects changes in `publish`.  
10. **Site published** – The plugin updates the live site from `publish`.

---

## Step-by-Step Table

| **Step**                             | **Action**                                                                      | **Example Commands**                                                                               |
| ------------------------------------ | ------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| 1. Pull official main                | Update your local `main` to match the remote.                                   | ```bash<br>git checkout main<br>git pull --rebase origin main<br>```                               |
| 2. Work on main                      | Make changes in Obsidian (notes, files, etc.).                                  | *(No Git commands yet)*                                                                            |
| 3. Commit and push                   | Stage, commit, and push your local changes to `origin/main`.                    | ```bash<br>git add .<br>git commit -m "Local changes"<br>git push origin main<br>```               |
| 4. Checkout publish                  | Switch from `main` to the `publish` branch.                                     | ```bash<br>git checkout publish<br>```                                                             |
| 5. Pull rebase from publish          | Ensure `publish` is up to date with its remote counterpart.                     | ```bash<br>git pull --rebase origin publish<br>```                                                 |
| 6. Merge or rebase main into publish | Incorporate your latest `main` changes into `publish`.                          | **Merge:**<br>```bash<br>git merge main<br>```<br>**Rebase:**<br>```bash<br>git rebase main<br>``` |
| 7. Resolve conflicts                 | If there are conflicts, edit the files to remove conflict markers, then commit. | ```bash<br>git add .<br>git commit -m "Resolve conflicts"<br>```                                   |
| 8. Push publish                      | Push the updated `publish` branch to the remote repository.                     | ```bash<br>git push origin publish<br>```                                                          |
| 9. Digital Garden plugin             | Automatically detects new commits on `publish` and updates the site.            | *(Plugin-driven; no direct command)*                                                               |
| 10. Site published from publish      | Your site is now live using the changes in `publish`.                           | *(Result of plugin deployment)*                                                                    |

---

### Key Points

- **Always pull or rebase `main`** from the remote repository (Step 1) before doing local work, so you have the official version.
- **Use `publish`** (or `gh-pages`) as a dedicated publishing branch, separate from your day-to-day editing on `main`.
- **Merge vs. Rebase**: Merging creates a merge commit, while rebasing creates a linear history. Choose based on your team’s preference.
- **Conflict Resolution**: If both `main` and `publish` changed the same lines, you must fix conflicts manually before committing.
- **Plugin Configuration**: Ensure the Digital Garden plugin is set to publish from the `publish` branch (or whichever branch you choose).

