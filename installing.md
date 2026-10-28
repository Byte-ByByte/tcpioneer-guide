# Windows Installation and Configuration

## Install the desktop app

Run the TCPIOneer Windows setup executable and follow the installer. It installs the TCPIOneer app and creates **TCPIOneer** shortcuts on the desktop and in the Start Menu. The server executable is bundled inside the installed app resources; it is not copied to the repository root. The app starts its local service and opens the human control page. For developers building from the repository, run:

```sh
npm run build:installer
```

The installer output is written to `release/TCPIOneer-Setup-<version>.exe`.

## Local use

By default, the Electron app binds the service to `127.0.0.1`. Open the control window and select **Connect here** to start a human session. You do not need the AI API token for local human control.

The Electron app creates a random API token on first start and saves it in its per-user `config.json` under `security.token` (on Windows, normally `%APPDATA%\tcpioneer\config.json`). Keep this file private. AI clients must send the token in the `Authorization: Bearer <token>` header.

## Enable remote human pairing

Remote access requires a network-reachable host and HTTPS with a certificate trusted by the connecting device. Stop TCPIOneer, then edit `config.json` to set the server bind address and TLS certificate paths:

```json
{
  "server": {
    "host": "0.0.0.0",
    "port": 3420,
    "tls": {
      "cert": "C:/certs/tcpioneer-fullchain.pem",
      "key": "C:/certs/tcpioneer-key.pem"
    }
  }
}
```

The certificate must be valid for the hostname used by remote browsers and for `localhost`, which the Electron app uses to open its local control page when TLS is enabled. Restart TCPIOneer after changing the configuration. On the host, open `/pc` and create a pairing code; the remote user redeems it on the HTTPS `/pc` page. See [Pairing codes](/guide/endpoints/pairing.md).

Do not expose the server over plain HTTP for remote use. Remote AI API calls also require HTTPS and a Bearer token header.

## CLI configuration

The CLI reads `config.json` from its working directory or distribution locations. Set `security.token` to a secret of at least 32 characters. If a config file contains a missing or shorter token, the CLI replaces it with a random token and writes the updated file. Configure TLS under `server.tls` with `cert` and `key` paths.
