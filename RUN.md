# Run the full app on Windows

**Double-click `run.cmd` in the extracted project folder.** It sets up the backend and frontend, starts both, and opens the chat in your browser. You can also start it from PowerShell in that folder with one command.

```powershell
.\run.cmd
```

## First run

1. Right-click the project ZIP, choose **Extract All**, then open the **lyftr-chat** folder containing `run.cmd`.
2. Have two different API keys ready for the same model. The default is `openai/gpt-4o-mini`. If you use another provider, copy `.env.example` to `.env` and set `LLM_MODEL` before starting. The README lists the configuration options.
3. Run `run.cmd`. It checks for Python 3.12 and Node.js 22 or newer with npm. If either is missing, the launcher uses Windows Package Manager (`winget`) to install it. Windows may display an installer approval prompt. Internet access is required to download missing tools and packages.
4. The launcher creates `backend\.venv` and installs the backend dependencies there. It creates a root `.env` from the example if needed. If valid-looking keys are missing, type or paste each key and press Enter. **The input stays blank while you type.** Both keys are saved in the local, Git-ignored `.env`.
5. The launcher installs frontend packages and waits for both services. When the browser opens, send a message to check that your provider accepts the keys.

| What to open | Address |
| --- | --- |
| Chat interface | http://localhost:3000 |
| Backend readiness | http://127.0.0.1:8000/health |

## Stop and restart

Keep the launcher window open while chatting. Press **Ctrl+C** in that window to stop the app. If Command Prompt asks whether to terminate the batch job, press **Y**, then Enter. Run the same command next time. The launcher reuses installed packages and checks for dependency changes.

With the supplied settings, native Windows history is stored in `backend\data\app.db`. Refreshing the browser starts a new session. The launcher translates the example's Docker database path for native use without editing that setting in your file.

## If startup stops

| Message or symptom | What to do |
| --- | --- |
| Windows cannot find winget | Install or update **App Installer** through Microsoft Store and reopen the terminal. On a managed computer, you can install Python 3.12 and Node.js 22+ with npm through your approved software catalog, then rerun. |
| An installer was canceled or a download failed | Restore internet access or finish the runtime installer, then rerun the same command. |
| Port 3000 or 8000 is already in use | Stop the previous launcher with Ctrl+C. If using the Docker version, stop it with `docker compose down` in the project folder. |
| The browser did not open | Open http://localhost:3000 after the launcher prints the address. |
| Health is OK but chat says all providers unavailable | Check both keys, model access, available quota and the configured provider URL in `.env`. Restart after editing. Health confirms configuration and database access. A successful chat confirms live inference. |

For Docker, deployment, backend tests, or the cache and failover demonstration, see [README.md](README.md).
