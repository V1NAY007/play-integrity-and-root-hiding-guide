# Play Integrity and Root Hiding Guide

**By [@V1NAY007](https://github.com/V1NAY007)**

**Last Updated:** 21/06/2026

A complete guide to passing strong Play Integrity and properly hiding root, in order to use banking apps on a rooted device.

---

## 📋 Table of Contents

- [Scenarios](#scenarios)
- [Types of Root](#types-of-root)
- [Modules Required](#modules-required)
- [Extra Information Regarding Scenarios](#extra-information-regarding-scenarios)
- [Flashing Order](#flashing-order)
- [Module-Specific Settings](#module-specific-settings)
- [Extra Notes](#extra-notes)
- [Troubleshooting](#troubleshooting)

---

## Scenarios

| Scenario | Description | Example ROMs |
|---|---|---|
| **1** | Custom ROM with Fingerprint Spoofing (PIF), TrickyStore, and Sandbox built in | Axion, ASCP 5.5, etc. |
| **2** | Custom ROM with Fingerprint Spoofing (PIF) and only Sandbox built in | ASCP 5.4 |
| **3** | Custom ROM with only Fingerprint Spoofing (PIF) | — |
| **4** | Custom ROM / Port ROM with no built-in spoofing | — |

---

## Types of Root

### 1. Magisk
The original root manager, introduced by **TopJohnWu**, widely used in earlier years — though most users have since shifted to kernel-based root (KernelSU). Comes with Zygisk built in. Easy to install on non-GKI (4.xx) kernels as well.

> ⚠️ **Not Recommended**

- Does **not** require Meta Modules
- Examples: [Magisk](https://github.com/topjohnwu/Magisk), Magisk Alpha, [Weavemask](https://github.com/Pleasrlee/Weavemask)

### 2. KernelSU
A modern kernel-based root solution. Does not come with Zygisk built in. Non-GKI kernels need to be manually built with KernelSU support; GKI (5.xx+) kernels support direct installation.

> ✅ **Recommended**

- Requires Meta Modules *(Exception: SukiSU Ultra)*
- Examples: [KernelSU](https://github.com/tiann/KernelSU), [KernelSU Next](https://github.com/KernelSU-Next/KernelSU-Next), [SukiSU Ultra](https://github.com/SukiSU-Ultra/SukiSU-Ultra), KOWSU

### 3. APatch
Not well documented in this guide — limited firsthand experience with this option.

> ⚠️ **Not Recommended**

- [APatch](https://github.com/bmax121/APatch)

---

## Modules Required

> **Just download these modules — do not flash yet.** Flashing order is covered [below](#flashing-order).

### 1. Meta Modules
Pick **one**: [Hybrid Mount](https://github.com/Hybrid-Mount/meta-hybrid_mount), [Magic Mount](https://github.com/KernelSU-Modules-Repo/magic_mount_rs), [OverlayFS](https://github.com/KernelSU-Modules-Repo/meta-overlayfs) *(I use Hybrid Mount)*.

Required with KernelSU and its forks to use most modern modules that mount data.

> **Note:** Only required if you use KernelSU or its forks (except SukiSU Ultra).

### 2. Zygisk Framework
Pick **one**: [ReZygisk](https://github.com/PerformanC/ReZygisk), [Zygisk Next](https://github.com/Dr-TSNG/ZygiskNext) *(I use ReZygisk)*.

Required by many modules that depend on Zygisk, such as PIF and HMA-OSS.

> **Note:** Only required for Scenario 3 and 4.
> If using ReZygisk, also flash [**Treatwheel**](https://github.com/PerformanC/Treat-Wheel-Zygisk) to properly hide it.

### 3. Pixel Fingerprint Spoofing
Pick **one**: [Play Integrity Fork](https://github.com/osm0sis/PlayIntegrityFork), [Play Integrity Fix [INJECT]](https://github.com/KOWX712/PlayIntegrityFix) *(I use Play Integrity Fix [INJECT])*.

Spoofs the device fingerprint to a Pixel device on the latest security patch, so that keyboxes work properly.

> **Note:** Only required for Scenario 4.
> Requires Zygisk.

### 4. TEE Spoofing
Pick **one**: [TrickyStore](https://github.com/5ec1cff/TrickyStore), [TEE-Simulator](https://github.com/JingMatrix/TEESimulator), [TEE-Simulator-RS](https://github.com/Enginex0/TEESimulator-RS) *(I use TEE-Simulator-RS)*.

Spoofs TEE (Trusted Execution Environment) status as "bootloader locked" using a keybox, configurable per app via a target list.

> **Example:** Some banking apps (BHIM, Axis, Canara ai1) detect TEE spoofing and need to be excluded from the target list.
> **Note:** Only required for Scenario 2, 3, and 4.

### 5. Tricky Addon
Pick **one**: [TrickyAddon](https://github.com/KOWX712/Tricky-Addon-Update-Target-List), [TrickyAddon Enhanced](https://github.com/Enginex0/tricky-addon-enhanced) *(I use TrickyAddon Enhanced)*.

Provides an easy-to-use WebUI for managing the TEE spoofing module — target list and keyboxes — without manual config edits.

> **Note:** Optional, but recommended alongside a TEE spoofing module.

### 6. Applist Hiding
Pick **one**: [Hide My Applist (HMA)](https://github.com/Dr-TSNG/Hide-My-Applist), [HMA-OSS (Hide My Applist – Open Source)](https://t.me/buggychat/87330?single) *(I use HMA-OSS)*.

Hides rooted apps and root management tools from detection by other apps.

> **Note:** Only required for Scenario 3 and 4.
> Requires Zygisk.
> HMA OSS comes in two variants: Zygisk(Recommended and link provided) and LSposed.

---

## Extra Information Regarding Scenarios

1. Even in Scenario 1, 2, or 3, you can still use standalone Fingerprint Spoofing and TEE Spoofing modules by disabling the ROM's built-in fingerprint spoofing and TrickyStore. *(Not recommended.)*
2. Do **not** flash an Applist Hiding module if your ROM already has Sandbox built in — it already includes HMA-OSS functionality.

---

## Flashing Order

```
Meta Module → Zygisk → Pixel Fingerprint Spoofing → TEE Spoofing → Tricky Addon → Applist Hiding
```

---

## Module-Specific Settings

> Only modules used by the author are covered here. If a module/setting isn't mentioned, leave it at default.

### Pixel Fingerprint Spoofing

**PIF Inbuilt (Scenario 1, 2, 3):**
- Just fetch the latest Pixel fingerprint via the ROM's built-in spoofing menu.

**Play Integrity Fix [INJECT]:**
- Turn on **Spoof Build** and **Spoof Build (Play Store)**
- Tick **Auto Security Patch**
- Fetch a random fingerprint using **AutoPIF**

### TEE Spoofing

**TrickyStore Inbuilt (Scenario 1):**
- Insert a valid keybox
- Open the Target List and add **Play Store** and **Play Services** to pass Integrity
- Add any apps you want spoofed as "bootloader locked" to the Target List (e.g. banking apps)
- Force-stop Play Store after adding it to the target list or adding a new keybox

**TEE-Simulator-RS:**
- During flashing, choose **Auto** or **Manual** mode — Auto adds apps to the target list automatically as you install them; Manual requires adding them yourself
- Open the WebUI, tick **Play Store** and **Play Services**
- Tick banking apps and any other apps you want spoofed as "bootloader locked"
- Use the keybox automation option (⋮ menu) to automatically fetch valid keyboxes from your chosen sources *(this can be unreliable — untick it and use a custom keybox if needed)*
- Force-stop Play Store after adding it to the target list or adding a new keybox

### Applist Hiding

**Sandbox (Scenario 1 and 2):**
- Hide root managers and rooted apps: open Sandbox → select the app → enable **Hide**
- Spoof banking apps: select the app → under Spoof Settings, enable **ADB**, **Developer Options**, **Wireless Debugging** → under Sandbox Options, enable **Force Data Isolation**

**HMA-OSS:**
1. Open HMA-OSS from the app drawer
2. **Manage Templates** → Create a blacklist template → name it anything → edit the list of invisible apps → add apps to hide (root managers, rooted apps, etc.) → save the template
3. **Bulk Config Wizard** → Edit App Settings → enable **Hide On** → **Template Config** → under "Using 0 templates," tick the template you just created → under "Using 0 setting presets," tick **Developer Options**
4. Edit the list of applied apps and select all banking apps and any other apps you want to spoof

---

## Extra Notes

**App-specific settings:**

| App | Setting |
|---|---|
| BHIM UPI | Untick from TEE Spoofing |
| Axis Bank | Untick from TEE Spoofing |
| Canara ai1 | Untick from TEE Spoofing |

---

## Troubleshooting

**Play Integrity not showing Strong even after spoofing fingerprint and TEE:**
- Did you force-stop the app after spoofing?
- Is your keybox valid?
- Is your fingerprint valid?
