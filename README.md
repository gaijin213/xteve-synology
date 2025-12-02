# xteve-synology

**Unleash IPTV Power on Your Synology in Minutes—With Docker & Xteve!**

---

Welcome! This guide transforms your Synology NAS into a next-level IPTV proxy using [Xteve IPTV Proxy](https://github.com/xteve-project/xTeVe) and Docker. Stream live TV directly to **Jellyfin, Plex, or Emby**—with all the EPG (electronic program guide) goodness!

---

## ⚡ Requirements

- **Any Synology Hardware** (from budget to beast)
- **Docker** installed—grab it from Synology’s Package Center

---

## 🚀 Step-by-Step: Lightning Setup

> **In less time than it takes to brew coffee, your IPTV universe is LIVE and streaming!**

### 1. Open Synology’s Task Scheduler
- Create a **new scheduled task**.

### 2. Under General
- **Task:** Name it something punchy (e.g., `Xteve Install`)
- **User:** root (for Docker permissions)

### 3. Scheduler Tab
- **Run on the following date:** Leave as is (just don’t worry about it!)

### 4. Task Settings
- **Paste this one-liner into the “Run command”:**
  ```bash
  docker run -it -d \
    --name=xteve \
    --network=host \
    --restart on-failure:3 \
    -e PUID=1026 \
    -e PGID=100 \
    -e TZ=Europe/Vilnius \
    -v /volume1/docker/xteve:/home/xteve/conf \
    dnsforge/xteve:latest
  ```
  > _Adjust `PUID`, `PGID`, `TZ`, or volume path as needed for your setup!_

### 5. Save & Run
- Click **OK**, then right-click your new task and **Run** it.

### 6. Wait It Out
- Grab your drink—wait **3-5 minutes**. Let magic happen.

### 7. Access the Xteve Web UI
- Go to: `http://<Your-NAS-IP>:34400/web`

---

## 🔧 Xteve Initial Configuration

1. **Choose the "XEPG"** option when prompted.
2. **Add your IPTV M3U URL:**  
   Example:  
   ```
   http://your-iptv-provider-domain:port/get.php?username=iptvusername&password=iptvpassword&type=m3u_plus
   ```
3. **Add your XML EPG file:**  
   Example:  
   ```
   http://your-iptv-provider-domain:port/xmltv.php?username=iptvusername&password=iptvpassword&type=m3u_plus
   ```

---

## 🛠️ Connect Xteve to Jellyfin, Plex, or Emby

1. In your media server (Jellyfin, Plex, Emby):
    - **Live TV settings → Tuner Device → Select "M3U Tuner"**
2. Enter your Xteve M3U playlist:  
   ```
   http://<Your-Server-IP>:34400/m3u/xteve.m3u
   ```
3. For TV Guide/EPG (especially Jellyfin):
    - Add XML TV Guide:  
      ```
      http://<Your-Server-IP>:34400
      ```
4. **Refresh Guide Data**
5. Head to your media server’s Live TV menu – **Boom! Channels with full EPG are ready!**

---

## 🎉 That’s it—ENJOY!

Streaming has never been easier, cheaper, or more customizable. Have questions or want to share your killer setup? [Open an issue](https://github.com/gaijin213/xteve-synology/issues) or fork this repo!

> _From zero to streaming hero – with Synology, Docker, and Xteve!_

---
