<div align="center">

<img width="80" height="80" alt="Everything Search icon" src="https://github.com/user-attachments/assets/282f4fda-b42b-49a4-823b-a5f9691730a3" />

# Everything Search — Complete Mastery Guide

**The fastest file search on Windows, fully unlocked.**
Sub-second results across millions of files. Boolean logic, regex, date/size filters,
duplicate detection, network access, and CLI automation — all in one free tool.

[![Everything Version](https://img.shields.io/badge/Everything-1.4.1%2B-blue?style=flat-square)](https://www.voidtools.com/)
[![Platform](https://img.shields.io/badge/platform-Windows-lightgrey?style=flat-square)]()
[![License](https://img.shields.io/badge/license-Freeware-green?style=flat-square)](https://www.voidtools.com/)

<br/>

### 🎓 Interactive Slide Deck

<a href="https://htmlpreview.github.io/?https://github.com/Olexify/GuideFor---Everything_SearchEngine/blob/main/everything-search-mastery-guide.html">
  <img src="https://img.shields.io/badge/▶%20%20OPEN%20INTERACTIVE%20SLIDES-Click%20Here%20to%20Launch-FF6B35?style=for-the-badge&logo=html5&logoColor=white" alt="Open Interactive Slides" height="50"/>
</a>

<br/><br/>

> 💡 The HTML file shows *"Error loading page"* inside GitHub — that's normal.
> Use the button above to open the actual interactive presentation.

<br/>

<img width="100%" alt="preview" src="https://github.com/user-attachments/assets/a8bc8cef-c5c0-42ef-97f9-46c509b206f0" />

</div>
---



## 📖 Table of Contents

1. [Why Everything?](#-why-everything)
2. [Shortcuts & Interface](#️-shortcuts--interface)
3. [Boolean Operators](#-boolean-operators)
4. [Wildcards & Modifiers](#-wildcards--modifiers)
5. [Date Filters](#-date-filters)
6. [Size Filters](#-size-filters)
7. [Type Macros & Attributes](#️-type-macros--attributes)
8. [Advanced Functions](#-advanced-functions)
9. [Duplicate Detection](#-duplicate-detection)
10. [Content Search & Regex](#-content-search--regex)
11. [Filters, Bookmarks & Macros](#-filters-bookmarks--macros)
12. [CLI & Search Commands](#️-cli--search-commands)
13. [Network, HTTP & ETP](#-network-http--etp)
14. [Power Search Recipes](#-power-search-recipes)

---

## ⚡ Why Everything?

Everything indexes the **Windows MFT (Master File Table)** directly - the same low-level index the OS itself uses - instead of crawling files like Windows Search does.

| Feature | Everything | Windows Search |
|---|---|---|
| Initial index time | **~1 second** (SSD) | Minutes to hours |
| RAM usage | **~6 MB** | 50–200 MB |
| Results while typing | **Instant** | Delayed |
| Regex support | ✅ Full PCRE | ❌ |
| Network/NAS indexing | ✅ | Limited |
| CLI tool (`es.exe`) | ✅ | ❌ |

> **Download:** [voidtools.com](https://www.voidtools.com/)

---

## ⌨️ Shortcuts & Interface

### Global Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| `Ctrl+F` | Focus search box |
| `Ctrl+T` | New search tab |
| `Alt+Home` | Clear search / go home |
| `F3` | Focus results list |
| `Ctrl+Enter` | Open containing folder |
| `Ctrl+C` | Copy full path to clipboard |
| `Ctrl+Shift+C` | Copy filename only (no path) |
| `Ctrl+1` … `Ctrl+5` | Sort by Name / Path / Size / Ext / Date |
| `Ctrl+,` | Open Options / Settings |
| `F5` | Force re-index (after mounting a drive) |
| Right-click | Full Windows Explorer context menu |

### 💡 Column Tips
- Right-click any column header to add **Date Created**, **Date Accessed**, **Attributes**, **Path**
- Drag columns to reorder
- Click a column header to toggle sort direction

---

## 🔣 Boolean Operators

Everything uses a simple inline syntax - no special mode needed.

| Operator | Symbol | Meaning | Example |
|---|---|---|---|
| AND | `SPACE` | Both terms must appear | `report 2026` |
| OR | `\|` | Either term matches | `jpg \| png` |
| NOT | `!` | Exclude this term | `report !backup` |
| Group | `< >` | Combine complex logic | `<jpg \| png> 2026` |
| Exact phrase | `" "` | Whole string match | `"meeting notes"` |

### Real-World Example

```
<jpg | png> holiday 2025 !thumb
```
*Images from holiday 2025, excluding thumbnails.*

---

## 🃏 Wildcards & Modifiers

### Wildcard Characters

| Pattern | Meaning | Example |
|---|---|---|
| `*` | Zero or more characters | `*.ini` |
| `?` | Exactly one character | `report_?.pdf` |
| `**` | Match across path separators (deep search) | `C:\**\config` |

### Search Modifiers

| Modifier | Meaning | Example |
|---|---|---|
| `case:` | Case-sensitive matching | `case:README` |
| `regex:` | Full regular expression (filename) | `regex:[0-9]{4}` |
| `path:` | Match in full path, not just name | `path:Config *.ini` |
| `wfn:` | Whole filename match only | `wfn:setup.exe` |
| `wholeword:` | Match whole word only | `wholeword:log` |
| `nopath:` | Disable `path:` prefix for this term | `path:docs nopath:backup` |
| `file:` | Restrict to files only | `file: *.log` |
| `folder:` | Restrict to folders only | `folder:node_modules` |

### Power Combo

```
path:UE_5.8 case:regex:Windows.*Engine\.ini
```
*Case-sensitive regex inside a path filter - finds your `.ini` files precisely across all drives.*

---

## 📅 Date Filters

### Date Modifier Prefixes

| Modifier | Filters by |
|---|---|
| `dm:` | Date Modified |
| `dc:` | Date Created |
| `da:` | Date Accessed |
| `dr:` | Date Run (executables only) |

### Date Constants

```
today        yesterday      thisweek      lastweek
thismonth    lastyear       last7days     last30days     last365days
```

### Date Range Syntax

```
dm:2026/06/01..2026/06/30 *.pdf        → PDFs modified in June 2026
dm:>2025/01/01 .log                    → All logs modified after Jan 1, 2025
dc:thisweek !.tmp                      → Files created this week, excluding temp files
```

---

## 📦 Size Filters

### Operators

| Syntax | Meaning | Example |
|---|---|---|
| `size:>N` | Larger than N (bytes/kb/mb/gb) | `size:>100mb` |
| `size:<N` | Smaller than N | `size:<1kb` |
| `size:A..B` | Inclusive range | `size:2mb..10mb` |
| `size:empty` | Zero-byte files | `size:empty *.log` |

### Named Size Constants

| Constant | Range |
|---|---|
| `tiny` | 1 byte – 10 KB |
| `small` | 10 KB – 100 KB |
| `medium` | 100 KB – 1 MB |
| `large` | 1 MB – 16 MB |
| `huge` | 16 MB – 128 MB |
| `gigantic` | 128 MB+ |

### Example

```
size:>500mb !.tmp dm:thismonth
```
*Large files modified this month, excluding temp files.*

---

## 🗂️ Type Macros & Attributes

### Built-in Type Macros

| Macro | Covers |
|---|---|
| `audio:` | mp3, flac, wav, ogg, aac… |
| `video:` | mp4, mkv, avi, mov… |
| `image:` | jpg, png, gif, bmp, webp… |
| `doc:` | docx, pdf, txt, md, xlsx… |
| `exe:` | exe, msi, bat, cmd |
| `zip:` | zip, rar, 7z, tar, gz |
| `font:` | ttf, otf, woff, woff2 |

### File Attributes

| Flag | Meaning |
|---|---|
| `attrib:H` | Hidden files |
| `attrib:S` | System files |
| `attrib:R` | Read-only |
| `attrib:E` | Encrypted |
| `attrib:C` | Compressed |
| `attrib:HSR` | Combine multiple flags |
| `runasadmin:` | Requires elevation |

### Example

```
attrib:H !attrib:S image:
```
*Hidden image files that are NOT system files - finds secret photos.*

---

## 🔬 Advanced Functions

| Function | Purpose | Example |
|---|---|---|
| `depth:N` | Limit folder nesting depth | `depth:1 *.ini` |
| `parent:` | Match a specific parent folder name | `parent:Config` |
| `child:` | Folder that contains a specific child | `child:package.json` |
| `empty:` | Empty files or empty folders | `empty:folder:` |
| `len:N` | Filename length equals N characters | `len:8 *.exe` |
| `count:N` | Folders with exactly N children | `count:0 folder:` |
| `width:` / `height:` | Image dimensions in pixels | `width:>3840` |
| `bitdepth:` | Image bit depth | `bitdepth:32` |
| `runcount:>N` | How many times an exe was run | `runcount:>100` |

### Example

```
child:package.json depth:3
```
*Find all Node.js projects within 3 folder levels deep.*

---

## 💯 Duplicate Detection

| Filter | Logic | Use Case |
|---|---|---|
| `dupe:` | Name + Size + Date all match | Finds likely exact duplicates |
| `sizedupe:` | Same size only | Catches renamed copies |
| `namepartdupe:` | Filename stem matches | Same base name, different extension |
| `dmdupe:` | Same Date Modified only | Files touched in same batch operation |

### Examples

```
image: dupe:             → Duplicate images (exact)
video: sizedupe:         → Videos with same file size (possibly renamed)
path:G:\ dupe:          → All duplicates on the G: drive
```

---

## 🧬 Content Search & Regex

### Content Search (inside files)

```
content:"api_key" *.env              → Find .env files containing "api_key"
utf8content:"TODO" *.ts              → UTF-8 encoded TypeScript files with TODO comments
```

> ⚠️ **Performance Note:** `content:` reads every matched file from disk - very slow on large drives.
> **Always combine with a path or type filter:**
> ```
> path:D:\Projects content:"TODO"
> ```

### Regex on Filenames (instant - no disk scan)

```
regex:^(2025|2026).*\.pdf$          → PDFs starting with 2025 or 2026
regex:[Cc]onfig[0-9]+\.ini          → Numbered config files, any case
```

Regex operates on the **filename only** (not content) and uses PCRE syntax.

---

## 📎 Filters, Bookmarks & Macros

### Custom Filters
Create at **Tools → Options → Filters**. Assign a name and a search query. The filter appears in the dropdown left of the search box.

```
UE5 Configs  →  path:EpicGames *.ini
Big Videos   →  video: size:huge
Recent Docs  →  doc: dm:last7days
```

### Bookmarks
Save any search via **Bookmarks → Add Bookmark**. Assign a keyboard shortcut. Bookmarks persist across restarts.

### Search Macros (Aliases)
Create at **Tools → Options → Search → Macros**. Map a short keyword to a full query:

```
ini    →  ext:ini
ue5    →  path:E:\EpicGames
bigvid →  video: size:huge
```

### Saved Searches (EFU)
**File → Export** saves any search as an `.efu` (Everything File URL) file. EFU files can be re-imported, shared with teammates, or used as virtual folders.

---

## 🖥️ CLI & Search Commands

### In-App Commands (type in the search box)

```
about:config     → Open raw config editor
about:rebuild    → Force full MFT re-index
about:update     → Check for updates
/close           → Exit the app
/restart         → Restart the Everything service
```

### Windows CLI (`es.exe`)

```bash
es.exe "*.ini" -path "EpicGames"          # .ini files under EpicGames
es.exe -size -10mb -ext exe               # Executables smaller than 10 MB
es.exe -export-csv output.csv "*.log"     # Export all .log file paths to CSV
es.exe "*.log" -n 20                      # Limit to 20 results
es.exe "path:D:\Projects" -p             # Print full paths
es.exe -r "regex:Config[0-9]+\.ini"      # Regex mode
```

### Export Formats
**File → Export** supports `.efu`, `.csv`, `.txt`. Use CSV output with PowerShell or Python for bulk file automation.

---

## 🌐 Network, HTTP & ETP

### HTTP Server (Browser Access)
Enable at **Tools → Options → HTTP Server**. Default port: 80.

```
http://192.168.x.x:80
```

Access Everything from any browser on your LAN - phone, tablet, other PCs. Supports full search + file download links. No client app required.

> 🔐 **Security:** Always set username/password in Options. Never expose the port to the internet without authentication.

### ETP Protocol (PC-to-PC)
**Everything Transport Protocol** - TCP-based, lets another PC running Everything connect to your full index.

- Server: **Tools → Options → ETP/FTP Server**
- Client: **Tools → Connect to ETP Server**

### Network Drives & NAS
Add UNC paths or mapped drives at **Tools → Options → Indexes**:

```
\\NAS01\Media   →   added as a virtual index
```

Requires read permission on the share. Everything will index those paths alongside local drives.

---

## 🚀 Power Search Recipes

Real queries for real workflows - copy, paste, adapt.

```bash
# 🎮 UE5 .ini Files Across All Drives
path:Config case:regex:Windows.*Engine\.ini

# 🗑️ Empty Folders (Disk Cleanup)
empty:folder:

# 🎬 Large Videos Modified This Month
video: size:huge dm:thismonth

# 🔍 Hidden Images (not system files)
image: attrib:H !attrib:S

# 🗄️ Backup Duplicates on G: Drive
path:G:\ dupe:

# 🧹 Node Modules Folders (Disk Hogs)
folder: wfn:node_modules

# 📄 Documents from Q1 2026
doc: dm:2026/01/01..2026/03/31

# ⚙️ Numbered Config Files (any case)
regex:[Cc]onfig[0-9]+\.ini

# 🔐 .env Files Containing Secrets
content:"api_key" *.env

# 📦 Large ZIP Archives, Not Recently Touched
zip: size:>200mb !dm:last30days
```

---

## 📚 Official Resources

| Resource | Link |
|---|---|
| Official site | [voidtools.com](https://www.voidtools.com/) |
| Full syntax docs | [voidtools.com/support/everything/searching](https://www.voidtools.com/support/everything/searching/) |
| Command-line reference | [voidtools.com/support/everything/command_line_interface](https://www.voidtools.com/support/everything/command_line_interface/) |
| HTTP server docs | [voidtools.com/support/everything/http](https://www.voidtools.com/support/everything/http/) |
| Forum | [forum.voidtools.com](https://forum.voidtools.com/) |

---

## 🎓 Interactive Presentation

This guide is also available as a **self-contained interactive HTML slide deck** - dark/light theme toggle, smooth animations, keyboard navigation.

```
everything-search-mastery.slides.html
```

- Navigate with **← →** arrow keys or swipe on mobile
- Toggle **☀️ / 🌙** for light and dark themes
- Works fully offline - single HTML file, zero dependencies

---

