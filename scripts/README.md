# Test-cycle automation

Add scripts here only for the repetitive, non-gameplay steps around a manual test session: deploying the mod to a local (and optionally remote) test environment, and collecting logs afterward. Starting the server/client, admin login, and in-game verification stay manual. Remove this folder if the project does not need it.

## Suggested scripts

- A pre-test setup script — mirrors `Contents/mods/<mod-id>/` into the local Project Zomboid client mods folder before a run, and optionally to a remote test server if a secrets file (see below) exists and is filled in. Do not clear logs as part of this step: Project Zomboid archives each session's files into a dated `logs_<date>` subfolder at startup, and clearing beforehand only destroys that archive.
- A post-test cleanup script — after the run, archives the local client logs and, if configured, pulls and archives the remote server's logs into the repository's gitignored [`../Logs/`](../Logs/) folder.
- A mid-session log-snapshot script — copies the current client logs into a timestamped snapshot without stopping the client or server. Project Zomboid's client debug log is capped in place with no rotation (observed around 4.3MB on one machine): once a session's log volume crosses that line, the engine silently drops its own oldest lines. A long or verbose diagnostic session can lose its early evidence this way; snapshot between test phases to keep it.

## Remote test-server secrets

If a script needs remote (for example SFTP) credentials for a dedicated test server, follow this pattern:

1. Commit an example file (such as [`server.env.example`](server.env.example)) with placeholder values only.
2. Keep the real file (`.env.server`, or similar) gitignored — never commit it or paste its contents into chat.
3. Have the script no-op the remote steps and only perform the local half until the real file exists with non-placeholder values.
4. If connecting over SFTP, verify the host's key fingerprint once and record it in the secrets file; some SFTP clients refuse to connect without it.

Wire any script added here into [`../AGENTS.md`](../AGENTS.md), [`../docs/DOCUMENTATION_OWNERSHIP.md`](../docs/DOCUMENTATION_OWNERSHIP.md), and [`../docs/TESTING.md`](../docs/TESTING.md) so the workflow stays discoverable.
