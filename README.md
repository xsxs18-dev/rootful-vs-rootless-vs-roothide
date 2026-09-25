# Rootful vs Rootless vs RootHide

A clear, side-by-side comparison of the three jailbreak filesystem layouts used on modern iOS, and which jailbreak is the best pick for each one.

> Information is current as of **September 2026**. Always double-check the official source of a jailbreak before using it on your device.

---

## Table of Contents

- [TL;DR](#tldr)
- [What Does "Root" Mean Here?](#what-does-root-mean-here)
- [Rootful](#rootful)
- [Rootless](#rootless)
- [RootHide](#roothide)
- [Full Comparison Table](#full-comparison-table)
- [Tweak Compatibility](#tweak-compatibility)
- [Best Jailbreaks](#best-jailbreaks)
- [Which One Should I Use?](#which-one-should-i-use)
- [Glossary](#glossary)
- [Disclaimer](#disclaimer)

---

## TL;DR

| | **Rootful** | **Rootless** | **RootHide** |
|---|---|---|---|
| Where jailbreak files live | Directly in `/` (system partition) | `/var/jb` | A random hidden folder, no `/var/jb` |
| Touches the system partition | Yes | No | No |
| Detection resistance | Poor | Medium | Best |
| Tweak availability | Legacy (iOS ≤ 14) tweaks | Largest modern library | Most rootless tweaks via auto-conversion |
| Best jailbreak | palera1n (rootful mode) | Dopamine | Relaxin |

---

## What Does "Root" Mean Here?

"Root" in these names does **not** mean root *user* privileges. Every one of these jailbreaks gives you root access.

It refers to **where on the filesystem the jailbreak installs its files** (package manager, tweaks, `apt`, `bash`, libraries, and so on):

- **Rootful**: into the real root filesystem `/`
- **Rootless**: into a separate directory, `/var/jb`
- **RootHide**: into a randomized, hidden directory that apps cannot easily find

This change was forced by Apple. Starting with iOS 15, the system partition is a **Signed System Volume (SSV)**: it is cryptographically sealed, so writing to it breaks the seal and the device will not boot normally. Jailbreak developers had to move everything out of `/`.

---

## Rootful

The classic way to jailbreak, used from the very first jailbreaks up to iOS 14.

### How it works

The jailbreak remounts the system partition as read-write and installs files directly into paths like `/usr/lib`, `/Library/MobileSubstrate`, and `/Applications`. On iOS 15 and later this is only possible through a **fakefs**: a writable copy of the system partition created on the data partition.

### Pros

- Full compatibility with the huge back catalogue of older tweaks (Cydia era)
- Tweaks and tools find files in their standard, expected locations
- Complete control over the whole filesystem

### Cons

- Modifies the system partition, so it carries more risk of a broken install
- On iOS 15+ it needs a fakefs, which uses several GB of storage
- Very easy to detect: banking apps and games just check for `/Applications/Cydia.app` or `/usr/lib/libsubstrate.dylib`
- Essentially only viable on checkm8 devices (A8–A11) for iOS 15+

### Example paths

```
/Library/MobileSubstrate/DynamicLibraries/
/usr/bin/apt
/Applications/Sileo.app
```

---

## Rootless

The modern standard since iOS 15, and what almost every current jailbreak and tweak targets.

### How it works

Nothing is written to the system partition. All jailbreak files go into a directory that is symlinked to `/var/jb`. Tweaks and packages are built for the `iphoneos-arm64` package architecture and load their files from `/var/jb/...`.

### Pros

- The system partition stays untouched and sealed
- Safer and easier to remove: deleting the jailbreak directory basically cleans it up
- No fakefs, so no extra storage cost
- The largest actively maintained tweak library today
- Supported by every major package manager (Sileo, Zebra) and by Theos

### Cons

- Old rootful tweaks must be updated or converted to work
- `/var/jb` is a fixed, well known path, so detection is simple: an app only needs to check whether `/var/jb` exists

### Example paths

```
/var/jb/Library/MobileSubstrate/DynamicLibraries/
/var/jb/usr/bin/apt
/var/jb/Applications/Sileo.app
```

---

## RootHide

A newer approach, built on top of rootless ideas, designed mainly to **hide the jailbreak from apps**.

### How it works

Just like rootless, the system partition is not touched. The difference is that the jailbreak root lives in a directory with a **random name** that changes per install, and there is **no `/var/jb` symlink**. Tweaks do not use hardcoded paths. Instead they call a `jbroot()` API to resolve the real location at runtime. Apps you have not explicitly chosen to inject simply cannot see the jailbreak.

Packages use the `iphoneos-arm64e` architecture. Most rootless tweaks can be converted automatically on-device with the **RootHide Patcher**.

### Pros

- Best jailbreak detection resistance of the three by design
- Banking apps, games, and work apps often run without any extra bypass tweak
- System partition stays untouched
- Randomized path means there is no fixed file for apps to look for
- Per-app control over which apps get tweaks injected

### Cons

- Smaller native tweak library than rootless
- Some tweaks need the RootHide Patcher, and a few do not convert cleanly
- Tweak developers have to use `jbroot()` for full native support

### Example paths

```
/var/containers/Bundle/Application/.jbroot-XXXXXXXXXXXXXXXX/usr/bin/apt
jbroot("/usr/bin/apt")
```

---

## Full Comparison Table

| Feature | Rootful | Rootless | RootHide |
|---|---|---|---|
| Jailbreak root | `/` | `/var/jb` | Random hidden directory |
| Modifies system partition | Yes | No | No |
| Needs fakefs on iOS 15+ | Yes | No | No |
| Extra storage required | High (fakefs) | Low | Low |
| Main iOS range | iOS ≤ 14, iOS 15+ on A8–A11 only | iOS 15+ | iOS 15+ |
| Package architecture | `iphoneos-arm` | `iphoneos-arm64` | `iphoneos-arm64e` |
| Legacy tweak support | Native | Needs update | Needs update or patcher |
| Modern tweak support | Poor | Best | Good (via patcher) |
| Jailbreak detection resistance | Poor | Medium | Excellent |
| Needs bypass tweaks for banking apps | Almost always | Often | Rarely |
| Risk of breaking the system | Higher | Low | Low |
| Ease of full removal | Harder (restore rootfs) | Easy | Easy |
| Package managers | Cydia, Sileo, Zebra | Sileo, Zebra | Sileo, Zebra (RootHide builds) |
| Tweak injection | Substrate / Substitute / ElleKit | ElleKit | ElleKit |

---

## Tweak Compatibility

| Tweak built for → | Rootful jailbreak | Rootless jailbreak | RootHide jailbreak |
|---|---|---|---|
| **Rootful** | ✅ | ❌ | ❌ |
| **Rootless** | ❌ | ✅ | ⚠️ Usually works after RootHide Patcher |
| **RootHide** | ❌ | ❌ | ✅ |

Tips:

- On rootless or RootHide, only install packages that list `iphoneos-arm64` or `iphoneos-arm64e`.
- Never force-install a rootful (`iphoneos-arm`) package on a rootless or RootHide setup.

---

## Best Jailbreaks

### Rootful

| Jailbreak | Supported | Type | Why |
|---|---|---|---|
| **palera1n** (rootful / fakefs mode) ⭐ | A8–A11, iOS 15.0 and newer | Semi-tethered (needs a computer) | The only realistic rootful option on modern iOS. Uses the unpatchable checkm8 bootrom exploit |
| **checkra1n** | A7–A11, iOS 12.0–14.8.1 | Semi-tethered | The legendary rootful jailbreak for older firmware |
| **unc0ver** | iOS 11.0–14.8 | Semi-untethered | The most widely used rootful jailbreak of its era |
| **Taurine** | iOS 14.0–14.8.1 | Semi-untethered | Clean, stable rootful option for iOS 14 |

**Pick:** palera1n in rootful mode on iOS 15+, checkra1n or unc0ver/Taurine if you are still on iOS 14 or lower.

### Rootless

| Jailbreak | Supported | Type | Why |
|---|---|---|---|
| **Dopamine** ⭐ | iOS 15.0–17.3.1 (arm64e), iOS 15.0–18.7.1 (A8–A13 / arm64), 26.0–26.0.1 (A12/A13) | Semi-untethered, no computer needed | The best and most polished jailbreak today. Very stable, widest device range, actively maintained (latest: 3.0.10) |
| **palera1n** (rootless mode) | A8–A11, iOS 15.0 and newer | Semi-tethered | Supports the newest firmware on checkm8 devices |

**Pick:** Dopamine. Use palera1n only if your A8–A11 device is on a firmware Dopamine does not cover.

### RootHide

| Jailbreak | Supported | Type | Why |
|---|---|---|---|
| **Relaxin** ⭐ | iOS 16.5.1–17.3.1 | Semi-untethered, no computer needed | My personal favourite. Modern, open source, built together with the RootHide developer, and full RootHide hiding out of the box |
| **Dopamine-RootHide** | iOS 15.0–16.x | Semi-untethered | The RootHide fork of Dopamine for iOS 15 and 16 |
| **RootHide Bootstrap** | iOS 15.0–17.0, A8–A17 Pro & M1/M2 | Semi-jailbreak via TrollStore | No kernel exploit needed. Great if you already have TrollStore |
| **palera1n-roothide** | A8–A11, iOS 15.0 and newer | Semi-tethered | RootHide on checkm8 devices |

**Pick:** Relaxin. In my opinion it is the best RootHide jailbreak available: clean, reliable, and it keeps your device hidden from detection with almost no extra setup.

---

## Which One Should I Use?

```
Do you need apps that block jailbroken devices (banking, games, work)?
│
├── Yes ──► RootHide  (Relaxin, Dopamine-RootHide, Bootstrap)
│
└── No
    │
    ├── Want the most tweaks and the most stable setup? ──► Rootless (Dopamine)
    │
    └── Need old iOS ≤ 14 tweaks on an A8–A11 device? ──► Rootful (palera1n rootful)
```

Summary:

- **Most people:** Rootless with Dopamine
- **Privacy / apps that detect jailbreaks:** RootHide with Relaxin
- **Legacy tweaks or old devices only:** Rootful with palera1n

---

## Glossary

| Term | Meaning |
|---|---|
| **SSV** | Signed System Volume. Apple's sealed, read-only system partition since iOS 15 |
| **fakefs** | A writable copy of the system partition used by rootful jailbreaks on iOS 15+ |
| **checkm8** | An unpatchable bootrom exploit for A5–A11 chips |
| **Semi-untethered** | After a reboot you re-run the jailbreak app on the device, no computer needed |
| **Semi-tethered** | After a reboot you need a computer to re-jailbreak |
| **ElleKit** | Modern tweak injection library used by rootless and RootHide jailbreaks |
| **TrollStore** | A tool that permanently installs apps with custom entitlements, used by some semi-jailbreaks |
| **`jbroot()`** | RootHide API that converts a normal path into the real, randomized jailbreak path |

---

## Disclaimer

Jailbreaking can void your warranty and may cause data loss or instability. Only download jailbreaks from their **official** sources, and always make a backup first. This repository is for educational purposes only.
