<h1 align="center">
Packetshare Pot 😃💰
</h1>

<div align="center">

[![Static Badge](https://img.shields.io/badge/GitHub-blue?style=flat&logo=github)](https://github.com/XternA/packetshare-reward)
[![Static Badge](https://img.shields.io/badge/License-purple?style=flat&logo=github)](https://github.com/XternA/packetshare-reward?tab=License-1-ov-file)
![GitHub package.json dynamic](https://img.shields.io/github/package-json/version/XternA/packetshare-reward?style=flat&logo=opencontainersinitiative&label=Image%20Tag&color=red)
[![Docker Stars](https://img.shields.io/docker/stars/xterna/packetshare-pot?logo=docker&label=Docker%20Stars)](https://hub.docker.com/r/xterna/packetshare-pot)
[![GitHub Repo stars](https://img.shields.io/github/stars/XternA/packetshare-reward?style=flat&logo=github&label=Stars&color=orange)](https://github.com/XternA/packetshare-reward)
[![Donate](https://img.shields.io/badge/Donate-PayPal-blue.svg?style=flat&logo=paypal)](https://www.paypal.com/donate/?hosted_button_id=32DCQ65QM5FNE)

If you like this project, don't forget to leave a star. ⭐

### Containerized Docker image for [Packetshare](https://bit.ly/47NcTVR) daily reward 💰

>**Note:** This built image comes with no warranty of any kind. By using this image you agree this License Aggrement in addition with Packetshare's T&C.

This is a simple Docker image for installing Packetshare's daily reward auto-claim script as a container.

</div>

## Pulling Image 🐋
**64-Bit Platform:** `linux/amd64` `linux/arm64`
```sh
docker pull ghcr.io/xterna/packetshare-pot
```

## Overview 😃
[**Packetshare-Pot**](https://bit.ly/47NcTVR) 😃💰 is a script (bot) powered by NodeJS and JavaScript to automatically claim the daily reward from [**Packetshare**](https://bit.ly/47NcTVR)😃.

The script bot is designed to run in a docker environment, allowing it to be deployed alongside the Packetshare docker container.

It uses very minimal resources, resulting in the CPU utilisation staying at idle **0%** the entire time unless logging into the website.
```
CONTAINER ID   NAME              CPU %     MEM USAGE / LIMIT   MEM %     NET I/O          BLOCK I/O        PIDS
0b7bfd54e811   packetshare-pot   0.00%     48.64MiB / 320MiB   15.20%    6.86MB / 250kB   45.7MB / 140MB   12
```

> [**Income Generator**](https://github.com/XternA/income-generator) comes pre-configured with this image. A tool which consolidates and earns passive income from multiple sources.

## Features 🚀
- Automatically log in and claim daily reward if threshold reached.
- Auto-wait until next event trigger.
- If error occurs, will auto restart the bot.

### Output 🖥️
This is what the script looks like when you inspect the output via `docker logs packetshare-pot`.
```
---------- Packetshare Reward Auto Claim ----------
Starting login process...
Logging in as example@abc.com
Logged into Packetshare 😃
---------------------------------------------------

Current Balance:   $ 5.14 💰
Earned Today:      $ 0.0104 🪙
Shared Today:      94.83MB 💻

Already claimed for today ✅
Waiting till next reward claim 🎁
Current logged time is 08:32:09
Next event trigger at 00:00:00
Wait time is 15 hour 27 minute ⏱️
```

## Usage 📃
Define the following environment variable to bootstrap the image.

| Variable | Description | Mandatory |
| :--- | :--- | :---: |
| **EMAIL**     | Your Packetshare email address    | YES |
| **PASSWORD**  | Your Packetshare password         | YES |

Or supply credentials in a Dotenv `.env` file.
```markdown
EMAIL=<email_address>
PASSWORD=<password_credential>
```

## Docker Deployment 🐋
### Compose
File: `compose.yml`
```yaml
services:
  packetshare-pot:
    container_name: packetshare-pot
    image: ghcr.io/xterna/packetshare-pot
    restart: unless-stopped
    environment:
      - EMAIL=$EMAIL
      - PASSWORD=$PASSWORD
    dns:
      - 1.1.1.1
      - 8.8.8.8
```

With Packetshare app docker image.
```yaml
services:
  packetshare:
    container_name: packetshare
    image: packetshare/packetshare
    restart: always
    environment:
      - EMAIL=$EMAIL
      - PASSWORD=$PASSWORD
    dns:
      - 1.1.1.1
      - 8.8.8.8

  packetshare-pot:
    container_name: packetshare-pot
    image: ghcr.io/xterna/packetshare-pot
    restart: unless-stopped
    environment:
      - EMAIL=$EMAIL
      - PASSWORD=$PASSWORD
    dns:
      - 1.1.1.1
      - 8.8.8.8
    depends_on:
      - packetshare
```

Execute where compose file is located.
```yaml
docker compose up -d
```

ℹ️ **Note:** If you apply resource limits such as CPU and RAM you need to set the following bare minimum:
```
  - cpu=0.8
  - mem_limit=350m
```
The script won't be able to run properly and will constantly timeout if the CPU and RAM limit is set lower than recommended. This is only required during the boot-up phase where it needs to spin up a headless browser to connect to the site. Resource is most intensive only during this phase.

### CLI
Using environment variable or Dotenv `.env` defined e.g.
```sh
docker run -d --restart unless-stopped --name packetshare-pot -e EMAIL=$EMAIL -e PASSWORD=$PASSWORD ghcr.io/xterna/packetshare-pot
```

Directly passing credentials.
```sh
docker run -d --restart unless-stopped --name packetshare-pot -e EMAIL=example@abc.com -e PASSWORD=pass123 ghcr.io/xterna/packetshare-pot
```
This will start the application in the background. The alias assigned is `packetshare-pot`.

## Like My Work? 🫶
Donations are warmly welcomed no matter how small and thank you very much. 😌
- **Bitcoin (BTC)** - `bc1qq993w3mxsf5aph5c362wjv3zaegk37tcvw7rl4`
- **Ethereum (ETH)** - `0x2601B9940F9594810DEDC44015491f0f9D6Dd1cA`
- **Binance Smart Chain (BSC)** - `0x2601B9940F9594810DEDC44015491f0f9D6Dd1cA`
- **Solana (SOL)** - `Ap5aiAbnsLtR2XVJB3sp37qdNP5VfqydAgUThvdEiL5i`
- **PayPal** - [@xterna](https://paypal.me/xterna)

## Disclaimer ⚠️
Disclaimer: This image is neither affiliated with nor endorsed by Packetshare. Use this image at your own risk and responsibility. By using this image, you agree to be automatically bound by the License Agreement associated with it.

The author does not provide any assurances, whether explicit or implicit, regarding the accuracy, completeness, or appropriateness of this image for specific purposes. The author shall not be held accountable for any damages, including but not limited to direct, indirect, incidental, consequential, or special damages, arising from the use or inability to use this image or its accompanying documentation, even if the possibility of such damages has been communicated.

By choosing to use this image, you acknowledge and assume all risks associated with its use. Additionally, you agree that the author cannot be held liable for any issues or consequences that may arise as a result of its usage.
