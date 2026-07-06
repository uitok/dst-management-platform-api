# DMP Windows Native Notes

This branch packages `dst-management-platform-api` as a Windows native backend. Run `dmp.exe`, then open the web UI in a browser.

## Quick Start

```powershell
.\dmp.exe
```

Default web address:

```text
http://127.0.0.1:80
```

If port 80 is occupied or you do not want to run on port 80, change the bind port:

```powershell
.\dmp.exe -bind 8080
```

Then open:

```text
http://127.0.0.1:8080
```

## Work Directory

On Windows, `DMP_HOME` defaults to the directory containing `dmp.exe`.

You can override it explicitly:

```powershell
.\dmp.exe -workdir D:\dst -bind 8080
```

Runtime paths are kept inside `DMP_HOME`:

```text
DMP_HOME\data\dmp.db
DMP_HOME\dst
DMP_HOME\steamcmd
DMP_HOME\dmp_files
DMP_HOME\klei\DoNotStarveTogether\Cluster_<id>
DMP_HOME\logs
```

## Windows Changes

- Windows uses native Go process management instead of `bash`, `screen`, and Linux pty.
- SteamCMD is installed under `DMP_HOME\steamcmd`.
- DST dedicated server is installed under `DMP_HOME\dst`.
- DST save/config files are written under `DMP_HOME\klei`, not the Windows user profile.
- WebSSH opens PowerShell on Windows.
- Empty `modoverrides.lua` content is normalized to `return {}` before game startup.
- The platform page opens the Overview tab by default.

## Build Artifact

GitHub Actions workflow `windows-native-build` builds and uploads:

```text
dmp-windows-amd64.zip
```

The zip contains:

```text
dmp.exe
WINDOWS.md
```

Run it from the directory you want to use as `DMP_HOME`, or pass `-workdir`.
