---
name: setup
description: Install and verify the Atlas Scout runtime required by this Claude plugin.
disable-model-invocation: true
---

# Set up Atlas Scout for Claude Code

The plugin requires a separately installed `atlas-scout` executable. Do not download or execute a
binary without the user's explicit approval.

1. Ask the user to review <https://atlasscout.dev/docs>, including the unsigned-preview disclosure
   and the platform-specific safety instructions.
2. If the user approves, download the supported installer for inspection:

   ```bash
   curl -fsSL https://atlasscout.dev/install.sh -o install.sh
   less install.sh
   ```

3. Run the inspected installer only after the user confirms:

   ```bash
   bash install.sh
   ```

4. Verify the active runtime and selected workspace:

   ```bash
   atlas-scout --version
   atlas-scout doctor --workspace /absolute/path/to/project
   ```

5. Start a new Claude Code session and run `/mcp`. The `atlas-scout` server should report as
   connected and should be identified as plugin-provided.

If Claude Code reports `spawn atlas-scout ENOENT`, add the installer-reported executable-link
directory to the environment that launches Claude Code, then start a new session. If a duplicate
manual server is active, remove or disable that registration before retrying.

To remove the plugin installed from the Zaguán Labs marketplace:

```bash
claude plugin uninstall atlas-scout@atlas-scout --scope user
claude plugin marketplace remove atlas-scout
```

Removing the plugin does not delete the Atlas Scout runtime or the disposable workspace indexes.
Follow the product documentation if the user also requests runtime removal.
