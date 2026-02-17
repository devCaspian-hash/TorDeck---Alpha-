# TorDeck (v1.1.15)

TorDeck is a cross-platform companion app for **TorBox**, built with **Expo + React Native + Expo Router**. It provides a single control panel across **iOS, Android, and Web** for adding downloads, organizing files, running automations, monitoring usage, and opening media.

> This README reflects the app state for the **1.1.15** feature set.

---

## Overview

TorDeck brings Torrent, Usenet, and Web downloads into one unified experience:

- **Unified dashboard** across sources
- **Library-first organization** with smart media classification
- **Powerful downloads manager** with advanced filtering + bulk actions
- **Automations engine** for scheduled rules and guardrails
- **Notifications center** merging remote + app-generated events
- **Stats & analytics** for activity, size, and source/category breakdowns
- **Settings & account insights** including usage, plan info, and preferences

---

## What’s Included in 1.1.15

- **Unified multi-source dashboard** for Torrent, Usenet, and Web downloads
- **Expanded downloads filtering** (status, source, media category, file type, age, size, file count, date sort)
- **Bulk download actions** from the Downloads tab (multi-select workflows and batch link generation)
- **Library quick-add actions** for Magnet, Info Hash, Web URL, and NZB input
- **Smart media classification** with local category override support
- **Audiobook grouping + detail flow** with per-track navigation and quick link actions
- **In-app notification center** combining TorBox notifications with app-generated notifications
- **Automation engine + presets** with polling execution, manual run support, and guardrails for risky actions
- **Default tab preference** in settings
- **Live account usage panel** (plan, usage, renewal/expiry, referral link)
- **Enhanced stats page** with source/category breakdowns and recent grouped activity

---

## Core Features

### 1) Account connection

- Connect using a TorBox API token
- Validates the token on connect (`/user/me`)
- Secure token storage per platform (native secure storage with web fallback)
- Automatic reconnect on app launch when a valid token is present

### 2) Unified library + classification

- Aggregates content from:
  - `torrent/mylist`
  - `usenet/mylist`
  - `webdl/mylist`
- Builds a unified file index across sources
- Auto-classifies items into:
  - Audiobooks
  - Music
  - Video
  - eBooks
  - Games
  - Other
- Supports **local category overrides** for user-corrected classification

### 3) Library experience

- Two viewing modes:
  - **Categories** (high-level browsing)
  - **All Files** (flat file-level browsing)
- Instant search filtering
- Expandable section for active/in-progress downloads
- Quick Add entry points to add-content flow
- Notification bell with unread indicator and modal list

### 4) Downloads manager

A full downloads workspace for every source (torrent / usenet / web):

- Source tabs and status filters
- Advanced filtering:
  - Media category
  - File type
  - Age
  - Size band
  - File count
  - Date sorting
- Item-level actions:
  - Open details
  - Generate download link
  - Copy/share link
  - Delete item
- Selection mode for **bulk operations**

### 5) Add content

Supports primary TorBox inputs from a single modal flow:

- Magnet link
- Torrent info hash
- Direct web URL
- NZB URL

Includes content-type selection, validation, loading states, and success handoff back to the main UI.

### 6) Automations (rule engine)

A local rule system that can trigger actions on a schedule:

- Presets + custom rules
- Poll-based execution loop
- Manual run support
- Scope control (`all`, `torrent`, etc.) and condition matching
- Built-in action support such as:
  - Pause / resume
  - Reannounce torrent
  - Delete download
  - Request download link
  - Create stream link
  - Notify user
- Guardrails for risky actions (e.g., destructive presets are flagged)

### 7) Notifications

Two notification streams are merged in-app:

- TorBox notifications from the API
- App-generated notifications (e.g., automation runs, newly completed downloads)

Users can dismiss individual notifications or clear all.

### 8) Stats & analytics

The Stats tab provides snapshot + drilldown:

- Total items and total size
- Completed and active counts
- Error count
- Source distribution (torrent/usenet/web)
- Category distribution (counts + bytes)
- Recent grouped activity with navigation into details

### 9) Settings + profile insights

Settings includes account and app behavior controls:

- User email, plan badge, subscription status
- Monthly and lifetime usage
- Usage progress indicator (when cap data is available)
- Last sync timestamp + manual refresh
- Referral link/code access
- Default startup tab selection
- Disconnect / clear auth state

### 10) Audiobook support

- Dedicated audiobook detail route
- Grouped tracks by parent download
- Track-level navigation
- Quick link actions (generate/copy/share)
- Delete full audiobook download from detail view

---

## Tech Stack

- **Expo / React Native** (iOS, Android, Web)
- **Expo Router** (file-based navigation)
- **TypeScript**
- **TanStack React Query** (server-state + cache invalidation)
- **AsyncStorage + context/hooks** (app-local state)
- Optional web proxy layer for browser API requests

---

## Project Structure

```text
app/
  (tabs)/
    (library)/
    automations/
    downloads/
    stats/
    settings/
  connect.tsx
  add-content.tsx
  download-detail.tsx
  audiobook-detail.tsx
  item/[id].tsx

hooks/
  useAuth.ts
  useLibrary.ts
  useAutomations.ts
  useSettings.ts
  useNotifications.ts
  useCategoryOverrides.ts

services/
  torbox-api.ts
  mediaTranscode.ts

netlify/edge-functions/
  torbox-proxy.ts
