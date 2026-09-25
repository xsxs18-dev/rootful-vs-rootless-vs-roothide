# Rootful vs Rootless vs RootHide

A simple guide for beginners: what these three words mean, how they are different, and which jailbreak you should use.

> Up to date as of **September 2026**.

---

## The Short Version

When you jailbreak your iPhone, the jailbreak has to put its files somewhere. The only real difference between **rootful**, **rootless** and **RootHide** is **where those files go**.

| | Rootful | Rootless | RootHide |
|---|---|---|---|
| Where the files go | Inside the iPhone's system | In a separate folder | In a secret folder with a random name |
| Safe for your system | ⚠️ Less safe | ✅ Safe | ✅ Safe |
| Hidden from banking apps and games | ❌ No | ⚠️ Sometimes | ✅ Yes, mostly |
| Number of tweaks | Old tweaks only | ✅ The most | Most rootless tweaks work too |
| Best jailbreak | palera1n | Dopamine | Relaxin |

---

## An Easy Way to Picture It

Think of your iPhone as a **house**.

- 🏠 **Rootful** puts your jailbreak stuff **all over the house**: in the kitchen, the living room, everywhere. It is easy to use, but anyone who walks in can see it, and you might damage something.
- 📦 **Rootless** puts all your stuff **in one box in the garage**. The house stays clean, but everyone knows where the box is (`/var/jb`), so apps can still check for it.
- 🕵️ **RootHide** puts your stuff **in a hidden room with a secret door**, and the door is in a different place on every phone. Apps walking through the house do not find anything.

---

## Rootful

The **old** way to jailbreak. It was used until iOS 14.

- The jailbreak writes its files straight into the iPhone's system.
- Since iOS 15, Apple locks the system, so rootful only works on older iPhones (iPhone 6s to iPhone X) and needs extra storage.
- Apps can detect it very easily.

**Good for:** old iPhones and old tweaks.
**Not good for:** most people today.

---

## Rootless

The **normal, modern** way to jailbreak, used since iOS 15.

- The system is not touched at all. Everything goes into one folder called `/var/jb`.
- Safer, and easy to remove.
- Almost every new tweak is made for rootless.
- Some apps can still notice it, because they know the folder `/var/jb`.

**Good for:** most people. The most tweaks and the most stable setup.

---

## RootHide

The **hidden** way to jailbreak.

- Works like rootless, but the jailbreak folder gets a **random name** and is hidden.
- Banking apps, games and work apps usually cannot tell that your phone is jailbroken, often **without any extra bypass tweak**.
- Most rootless tweaks work too. Some need to be converted first with the built-in **RootHide Patcher** (just a few taps).

**Good for:** people who want to use banking apps or games that block jailbroken phones.

---

## Will My Tweak Work?

| Tweak made for... | On Rootful | On Rootless | On RootHide |
|---|---|---|---|
| Rootful | ✅ | ❌ | ❌ |
| Rootless | ❌ | ✅ | ✅ Usually, after the RootHide Patcher |
| RootHide | ❌ | ❌ | ✅ |

---

## The Best Jailbreaks

### 🏆 Rootful: palera1n

- **iPhones:** iPhone 6s to iPhone X (A8–A11 chips)
- **iOS:** 15.0 and newer
- **Note:** you need a computer every time you restart your phone

For very old phones on iOS 14 or lower: **checkra1n**, **unc0ver** or **Taurine**.

### 🏆 Rootless: Dopamine

- **iOS:** 15.0 to 17.3.1 on most iPhones, and up to 18.7.1 on iPhone 6s to iPhone 11
- **Note:** no computer needed. After a restart, just open the app and tap jailbreak again
- The best and most stable jailbreak right now

Alternative: **palera1n** (rootless mode) for iPhone 6s to iPhone X on newer iOS.

### 🏆 RootHide: Relaxin ⭐ My Favourite

- **iOS:** 16.5.1 to 17.3.1
- **Note:** no computer needed. After a restart, just open the app again
- Open source, very clean and easy to use, and your jailbreak stays hidden with almost no setup

In my opinion, Relaxin is the best RootHide jailbreak there is.

Other RootHide options:
- **Dopamine-RootHide** for iOS 15 and 16
- **RootHide Bootstrap** for iOS 15.0 to 17.0 (needs TrollStore)
- **palera1n-roothide** for iPhone 6s to iPhone X

---

## Which One Should I Pick?

```
Do you want to use banking apps or games that block jailbroken phones?
│
├── Yes ──► RootHide  →  Relaxin
│
└── No  ──► Rootless  →  Dopamine
```

Rootful is only worth it for older iPhones or old tweaks.

---

## Small Dictionary

| Word | What it means |
|---|---|
| **Tweak** | A small add-on that changes how your iPhone looks or works |
| **Semi-untethered** | After restarting, you open the jailbreak app on your phone again. No computer needed |
| **Semi-tethered** | After restarting, you need a computer to jailbreak again |
| **Sileo / Zebra** | App stores for tweaks |
| **TrollStore** | A tool that lets you install special apps permanently |

---

## Before You Start

- ✅ Make a **backup** of your iPhone first.
- ✅ Only download jailbreaks from their **official** websites or GitHub pages.
- ⚠️ Jailbreaking can void your warranty and may cause problems. You do it at your own risk.

This guide is for learning purposes only.
