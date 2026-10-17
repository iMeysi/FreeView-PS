# FreeView-PS
---
# English README

# AetherView — FreeView PowerShell Edition

> A PowerShell menu interface for managing and running Aether on Windows  
> Includes WARP + Psiphon CDN, Psiphon-only, Gaming, Chain, Tor, and Psiphon Direct modes.

---

## Overview

**AetherView** is a PowerShell script that simplifies running the [Aether](https://github.com/CluvexStudio/aether) core. This project is not the tunnel core itself; it is an interactive menu for installing/updating Aether, selecting connection modes, and configuring CDN fronting, fragmentation, SNI, Tor, Gaming, and Chain settings.

The script is designed for **Windows PowerShell 5.1** and stores its configuration here:

```text
%USERPROFILE%\.freeview\config.json
```

The Aether executable is stored here:

```text
%USERPROFILE%\.freeview\aether.exe
```

After a successful run, a SOCKS5 proxy is available at:

```text
127.0.0.1:1313
```

---

## Features

- Full interactive Windows menu
- Automatic Aether installation and update from GitHub
- Configuration persistence in `config.json`
- Multiple connection modes:
  - WARP + Psiphon CDN Fronting
  - Psiphon-only CDN Fronting
  - Gaming Mode (WARP-in-WARP)
  - Gaming + Psiphon Chain
  - Tor + CDN Fronting
  - Psiphon Direct with region selection
- CDN Edge IP list management
- SNI and Fragment toggles
- Fragment size and delay configuration
- Tor mode, bridges, and custom bridge lines
- Gaming/Chain protocol, exit, scan, and noize settings
- Aether status display and stop control
- Port-in-use checks before launch

---

## Requirements

- Windows 10 or 11
- Windows PowerShell 5.1
- Internet access to download Aether
- Permission to run PowerShell scripts

To run the script in the current session:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\FreeView.ps1
```

> If you saved the script under another name, replace `FreeView.ps1` with that name.

---

## Quick Start

1. Save `FreeView.ps1` on your system.
2. Open PowerShell and navigate to the file location.
3. Run:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\FreeView.ps1
```

4. Choose **1) Install / Update Aether**.
5. Select a connection mode. For a typical start, choose **2) Start (WARP + Psiphon CDN)**.
6. Once running, SOCKS5 is available at `127.0.0.1:1313`.

---

## Main Menu

| Option | Description |
|---|---|
| 1 | Install or update Aether |
| 2 | Start WARP + Psiphon CDN |
| 3 | Start Psiphon-only CDN |
| 4 | Start Gaming Mode |
| 5 | Start Gaming + Psiphon Chain |
| 6 | Start Tor + CDN Fronting |
| 7 | Start Psiphon Direct by region |
| 8 | CDN / Fronting settings |
| 9 | Tor settings |
| 10 | Gaming settings |
| 11 | Chain settings — not fully implemented in the PowerShell version |
| 12 | Psiphon settings — not fully implemented in the PowerShell version |
| 13 | Advanced settings |
| 14 | Show current configuration |
| 15 | Stop Aether |
| 0 | Exit |

---

## Default Settings

| Key | Default | Description |
|---|---|---|
| `MAIN_PORT` | `1313` | Main SOCKS5 port |
| `PSIPHON_PORT` | `1314` | Internal Psiphon port |
| `CDN_SNI_ENABLED` | `no` | Custom SNI enabled |
| `FRAGMENT_ENABLED` | `yes` | Fragmentation enabled |
| `FRAGMENT_SIZE` | `8-24` | Fragment size |
| `FRAGMENT_DELAY` | `5-15` | Fragment delay |
| `TOR_MODE` | `tor` | Tor mode |
| `TOR_BRIDGES` | `auto` | Tor bridges mode |
| `TOR_BIND` | `127.0.0.1:1820` | Tor bind address |
| `GAMING_PROTO` | `gool-classic` | Gaming protocol |
| `GAMING_EXIT` | `DE` | Gaming exit region |
| `CHAIN_PROTO` | `gool-classic` | Chain protocol |
| `CHAIN_EXIT` | `!IR,AZ,RU` | Chain exit region |
| `CHAIN_WARP_UNDER` | `yes` | Use Psiphon under Chain |
| `PSIPHON_REGION` | `DE` | Psiphon region |
| `PSIPHON_MODE` | `cdn` | Psiphon mode |

Settings can be changed through the menus and are saved to `config.json`.

---

## Connection Modes

### 1) WARP + Psiphon CDN

Combines WARP with Psiphon in CDN fronting mode. This mode uses MASQUE and H2 and is suitable for general use.

### 2) Psiphon-only CDN

Runs only Psiphon in CDN fronting mode, without WARP.

### 3) Gaming Mode

Classic WARP-in-WARP mode focused on gaming. The default protocol is `gool-classic`, and it can be changed to `gool` or `wg`.

### 4) Gaming + Psiphon Chain

Combines Gaming with Psiphon Chain. If `CHAIN_WARP_UNDER` is `yes`, Psiphon is placed under Chain. Otherwise, reverse mode is used, and if `gool-classic` is selected, the script automatically switches to `masque`.

### 5) Tor + CDN Fronting

Runs Tor with CDN fronting. Tor modes:

- `tor-only`: Tor only
- `tor`: Tor with Psiphon CDN
- `tor-reverse`: Tor Reverse with Psiphon CDN

### 6) Psiphon Direct

Runs Psiphon directly with a selected region and mode. If mode is `cdn`, it uses H2, fragmentation, SNI, and CDN IPs.

---

## CDN Settings

In **8) CDN / Fronting Settings**, you can:

- View the CDN Edge IP list.
- Add new IPs.
- Enable or disable SNI.
- Enable or disable fragmentation.
- Change fragment size and delay.
- Edit `CDN_SETS`.

Default CDN IPs are defined in `CDN_EDGE_IPS` at the top of the script.

---

## Tor Settings

In **9) TOR Settings**, you can:

- Change `TOR_MODE` between `tor-only`, `tor`, and `tor-reverse`.
- Set `TOR_BRIDGES` to `auto`, `off`, or `custom`.
- In `custom` mode, separate bridge lines with `;`.

---

## Gaming Settings

In **10) Gaming Settings**, you can change:

- `GAMING_PROTO`
- `GAMING_EXIT`
- `GAMING_SCAN`
- `GAMING_NOIZE`

---

## Files and Paths

| Path | Description |
|---|---|
| `%USERPROFILE%\.freeview\config.json` | Configuration file |
| `%USERPROFILE%\.freeview\aether.exe` | Aether executable |
| `FreeView.ps1` | Main script |

---

## Troubleshooting

### The script does not run

If you get an Execution Policy error:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

### Aether does not download

- Check your internet connection and GitHub access.
- Download manually from:

```text
https://github.com/CluvexStudio/aether/releases
```

Then place the file here:

```text
%USERPROFILE%\.freeview\aether.exe
```

### Port is already in use

If you see a port-in-use message, change `MAIN_PORT` and `PSIPHON_PORT` from **13) Advanced Settings**.

### Aether does not stop

Use **15) Stop Aether**. If needed, close the `aether` process from Task Manager.

### Options 11 and 12 are incomplete

In the PowerShell version, Chain and Psiphon menus are not fully implemented and only show a notice. Use defaults or edit `config.json` manually.

---

## Limitations

- Windows and PowerShell 5.1 only.
- Depends on the Aether executable.
- Chain and Psiphon menus are incomplete in the current version.
- Behavior depends on the Aether version and supported parameters.
- Some networks may require CDN, SNI, or fragmentation adjustments.

---

## Security and Responsibility

- This project is only a menu interface and does not implement the tunnel core.
- Download Aether from the official source and inspect it when possible.
- Keep proxy ports bound to `127.0.0.1` and do not expose them publicly.
- Use this tool in compliance with local laws and network policies.
- You are responsible for how you use this project.

---

## Development

This project is currently a single-file PowerShell script. Possible improvements:

- Complete the Chain and Psiphon menus.
- Improve input validation.
- Add multiple configuration profiles.
- Add file logging.
- Add automatic Aether version comparison.
- Add a SOCKS5 health check and connection test.

---

## License

Choose a license for this project. For public release, **MIT** is a suitable option. Add it as a `LICENSE` file.

---

## Credits

- Core: [Aether](https://github.com/CluvexStudio/aether)
- PowerShell interface and menu: AetherView / FreeView PowerShell Edition

---

# README فارسی

# AetherView — نسخهٔ PowerShell پروژهٔ FreeView

> یک رابط منویی PowerShell برای مدیریت و اجرای Aether روی ویندوز  
> شامل حالت‌های WARP + Psiphon CDN، Psiphon-only، Gaming، Chain، Tor و Psiphon Direct.

---

## معرفی

**AetherView** یک اسکریپت PowerShell است که اجرای هستهٔ [Aether](https://github.com/CluvexStudio/aether) را ساده می‌کند. این پروژه خودش هستهٔ تونل نیست؛ بلکه یک منوی تعاملی برای نصب و به‌روزرسانی Aether، انتخاب حالت اتصال و تنظیم CDN Fronting، Fragment، SNI، Tor، Gaming و Chain است.

این اسکریپت برای **Windows PowerShell 5.1** طراحی شده و تنظیمات را در مسیر زیر ذخیره می‌کند:

```text
%USERPROFILE%\.freeview\config.json
```

فایل اجرایی Aether نیز در این مسیر نگهداری می‌شود:

```text
%USERPROFILE%\.freeview\aether.exe
```

پس از اجرای موفق، یک پروکسی SOCKS5 روی آدرس زیر در دسترس خواهد بود:

```text
127.0.0.1:1313
```

---

## ویژگی‌ها

- منوی تعاملی کامل برای ویندوز
- نصب و به‌روزرسانی خودکار Aether از GitHub
- ذخیره و بارگذاری تنظیمات در `config.json`
- پشتیبانی از چند حالت اتصال:
  - WARP + Psiphon CDN Fronting
  - Psiphon-only CDN Fronting
  - Gaming Mode (WARP-in-WARP)
  - Gaming + Psiphon Chain
  - Tor + CDN Fronting
  - Psiphon Direct با انتخاب منطقه
- مدیریت لیست IPهای CDN Edge
- فعال/غیرفعال کردن SNI و Fragment
- تنظیم اندازه و تأخیر Fragment
- تنظیم حالت Tor، پل‌ها و Bridgeهای سفارشی
- تنظیم پروتکل، خروجی، Scan و Noize برای Gaming و Chain
- نمایش وضعیت اجرا و توقف Aether
- بررسی اشغال بودن پورت‌ها قبل از اجرا

---

## پیش‌نیازها

- ویندوز 10 یا 11
- Windows PowerShell 5.1
- دسترسی به اینترنت برای دانلود Aether
- مجوز اجرای اسکریپت PowerShell

برای اجرای اسکریپت در همان Session:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\FreeView.ps1
```

> اگر اسکریپت را با نام دیگری ذخیره کرده‌اید، همان نام را در دستور بالا جایگزین کنید.

---

## شروع سریع

1. فایل `FreeView.ps1` را روی سیستم ذخیره کنید.
2. PowerShell را باز کنید و به پوشهٔ فایل بروید.
3. دستور زیر را اجرا کنید:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\FreeView.ps1
```

4. گزینهٔ **1) Install / Update Aether** را انتخاب کنید.
5. یکی از حالت‌های اتصال را انتخاب کنید. برای شروع معمولاً گزینهٔ **2) Start (WARP + Psiphon CDN)** مناسب است.
6. پس از اجرا، SOCKS5 روی `127.0.0.1:1313` در دسترس است.

---

## منوی اصلی

| گزینه | توضیح |
|---|---|
| 1 | نصب یا به‌روزرسانی Aether |
| 2 | اجرای WARP + Psiphon CDN |
| 3 | اجرای Psiphon-only CDN |
| 4 | اجرای Gaming Mode |
| 5 | اجرای Gaming + Psiphon Chain |
| 6 | اجرای Tor + CDN Fronting |
| 7 | اجرای Psiphon Direct بر اساس Region |
| 8 | تنظیمات CDN / Fronting |
| 9 | تنظیمات Tor |
| 10 | تنظیمات Gaming |
| 11 | تنظیمات Chain — در نسخهٔ PowerShell فعلاً کامل پیاده‌سازی نشده |
| 12 | تنظیمات Psiphon — در نسخهٔ PowerShell فعلاً کامل پیاده‌سازی نشده |
| 13 | تنظیمات پیشرفته |
| 14 | نمایش تنظیمات فعلی |
| 15 | توقف Aether |
| 0 | خروج |

---

## تنظیمات پیش‌فرض

| کلید | مقدار پیش‌فرض | توضیح |
|---|---|---|
| `MAIN_PORT` | `1313` | پورت SOCKS5 اصلی |
| `PSIPHON_PORT` | `1314` | پورت داخلی Psiphon |
| `CDN_SNI_ENABLED` | `no` | فعال بودن SNI سفارشی |
| `FRAGMENT_ENABLED` | `yes` | فعال بودن Fragment |
| `FRAGMENT_SIZE` | `8-24` | اندازه Fragment |
| `FRAGMENT_DELAY` | `5-15` | تأخیر Fragment |
| `TOR_MODE` | `tor` | حالت Tor |
| `TOR_BRIDGES` | `auto` | حالت پل‌های Tor |
| `TOR_BIND` | `127.0.0.1:1820` | آدرس Bind برای Tor |
| `GAMING_PROTO` | `gool-classic` | پروتکل Gaming |
| `GAMING_EXIT` | `DE` | منطقهٔ خروجی Gaming |
| `CHAIN_PROTO` | `gool-classic` | پروتکل Chain |
| `CHAIN_EXIT` | `!IR,AZ,RU` | منطقهٔ خروجی Chain |
| `CHAIN_WARP_UNDER` | `yes` | استفاده از Psiphon زیر Chain |
| `PSIPHON_REGION` | `DE` | منطقهٔ Psiphon |
| `PSIPHON_MODE` | `cdn` | حالت Psiphon |

تنظیمات از طریق منوها قابل تغییر هستند و در `config.json` ذخیره می‌شوند.

---

## حالت‌های اتصال

### 1) WARP + Psiphon CDN

ترکیب WARP با Psiphon در حالت CDN Fronting. این حالت از MASQUE و H2 استفاده می‌کند و برای استفادهٔ عمومی مناسب است.

### 2) Psiphon-only CDN

فقط Psiphon در حالت CDN Fronting اجرا می‌شود؛ بدون WARP.

### 3) Gaming Mode

حالت کلاسیک WARP-in-WARP با تمرکز روی Gaming. پروتکل پیش‌فرض `gool-classic` است و می‌تواند به `gool` یا `wg` تغییر کند.

### 4) Gaming + Psiphon Chain

ترکیب Gaming با Psiphon Chain. اگر `CHAIN_WARP_UNDER` روی `yes` باشد، Psiphon زیر Chain قرار می‌گیرد. در غیر این صورت حالت Reverse استفاده می‌شود و در صورت انتخاب `gool-classic` اسکریپت به‌صورت خودکار به `masque` سوییچ می‌کند.

### 5) Tor + CDN Fronting

اجرای Tor به همراه CDN Fronting. حالت‌های Tor:

- `tor-only`: فقط Tor
- `tor`: Tor به همراه Psiphon CDN
- `tor-reverse`: Tor Reverse به همراه Psiphon CDN

### 6) Psiphon Direct

اجرای مستقیم Psiphon با انتخاب Region و Mode. اگر Mode روی `cdn` باشد، از H2، Fragment، SNI و CDN IPها استفاده می‌شود.

---

## تنظیمات CDN

در منوی **8) CDN / Fronting Settings** می‌توانید:

- لیست IPهای CDN Edge را ببینید.
- IP جدید اضافه کنید.
- SNI را فعال یا غیرفعال کنید.
- Fragment را فعال یا غیرفعال کنید.
- اندازه و تأخیر Fragment را تغییر دهید.
- مقدار `CDN_SETS` را ویرایش کنید.

IPهای پیش‌فرض CDN در ابتدای اسکریپت داخل `CDN_EDGE_IPS` قرار دارند.

---

## تنظیمات Tor

در منوی **9) TOR Settings** می‌توانید:

- `TOR_MODE` را بین `tor-only`، `tor` و `tor-reverse` تغییر دهید.
- `TOR_BRIDGES` را روی `auto`، `off` یا `custom` بگذارید.
- در حالت `custom`، خطوط Bridge را با `;` جدا کنید.

---

## تنظیمات Gaming

در منوی **10) Gaming Settings** می‌توانید این مقادیر را تغییر دهید:

- `GAMING_PROTO`
- `GAMING_EXIT`
- `GAMING_SCAN`
- `GAMING_NOIZE`

---

## فایل‌ها و مسیرها

| مسیر | توضیح |
|---|---|
| `%USERPROFILE%\.freeview\config.json` | فایل تنظیمات |
| `%USERPROFILE%\.freeview\aether.exe` | فایل اجرایی Aether |
| `FreeView.ps1` | اسکریپت اصلی |

---

## عیب‌یابی

### اسکریپت اجرا نمی‌شود

اگر با خطای Execution Policy مواجه شدید:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

### Aether دانلود نمی‌شود

- اتصال اینترنت و دسترسی به GitHub را بررسی کنید.
- به‌صورت دستی از صفحهٔ Releases دانلود کنید:

```text
https://github.com/CluvexStudio/aether/releases
```

و فایل را در این مسیر قرار دهید:

```text
%USERPROFILE%\.freeview\aether.exe
```

### پورت اشغال است

اگر پیام اشغال بودن پورت نمایش داده شد، از منوی **13) Advanced Settings** پورت‌های `MAIN_PORT` و `PSIPHON_PORT` را تغییر دهید.

### Aether متوقف نمی‌شود

از گزینهٔ **15) Stop Aether** استفاده کنید. در صورت نیاز، از Task Manager پروسهٔ `aether` را ببندید.

### گزینه‌های 11 و 12 کامل نیستند

در نسخهٔ PowerShell، منوهای Chain و Psiphon به‌صورت کامل پیاده‌سازی نشده‌اند و فقط پیام راهنما نمایش می‌دهند. از مقادیر پیش‌فرض استفاده کنید یا `config.json` را دستی ویرایش کنید.

---

## محدودیت‌ها

- فقط برای ویندوز و PowerShell 5.1 نوشته شده است.
- به فایل اجرایی Aether وابسته است.
- منوهای Chain و Psiphon در نسخهٔ فعلی کامل نیستند.
- رفتار پروژه به نسخهٔ Aether و پارامترهای پشتیبانی‌شدهٔ آن وابسته است.
- دسترسی به برخی شبکه‌ها ممکن است نیاز به تنظیمات CDN، SNI یا Fragment داشته باشد.

---

## امنیت و مسئولیت

- این پروژه فقط یک رابط منویی است و هستهٔ تونل را خودش پیاده‌سازی نمی‌کند.
- فایل اجرایی Aether را از منبع رسمی دریافت کنید و در صورت امکان آن را بررسی کنید.
- پورت‌های پروکسی را روی `127.0.0.1` نگه دارید و به‌صورت عمومی Expose نکنید.
- استفاده از این ابزار باید مطابق قوانین محلی و قوانین شبکهٔ محل استفاده باشد.
- مسئولیت استفاده از پروژه با کاربر است.

---

## توسعه

این پروژه در حال حاضر به‌صورت یک اسکریپت PowerShell تک‌فایلی است. برای توسعهٔ بیشتر می‌توان:

- منوی Chain و Psiphon را کامل کرد.
- اعتبارسنجی ورودی‌ها را بهتر کرد.
- پشتیبانی از چند پروفایل تنظیمات اضافه کرد.
- خروجی لاگ به فایل اضافه کرد.
- بررسی خودکار نسخهٔ Aether و مقایسه با نسخهٔ نصب‌شده اضافه کرد.
- گزینهٔ تست اتصال و بررسی سلامت SOCKS5 اضافه کرد.

---

## مجوز

برای این پروژه یک مجوز مشخص انتخاب کنید. اگر قصد انتشار عمومی دارید، پیشنهاد می‌شود از مجوزی مانند **MIT** استفاده کنید و آن را در فایل `LICENSE` قرار دهید.

---

## قدردانی

- هستهٔ اصلی: [Aether](https://github.com/CluvexStudio/aether)
- رابط PowerShell و منو: AetherView / FreeView PowerShell Edition
