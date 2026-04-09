# OmniTra**KR** — Track Everything You Experience

A high-performance Laravel + Vue.js web application for tracking movies, TV shows, anime, manga, books, comics, games, board games, tabletop RPGs, music, podcasts, restaurants, and more — all in one place.

> **Note:** A detailed `ARCHITECTURE.md` file exists locally (gitignored) that explains how every part of the system fits together — Docker containers, module structure, request lifecycle, worker lifecycle, the fallback system, database layer, and a step-by-step guide for adding new content types. Run `git clone` then ask for the file separately.

---

## Project Overview

OmniTrakr is a modern SPA (Single Page Application) that acts as a personal hub for everything you watch, read, play, listen to, and experience. Each content type lives in its own dedicated hub, grouped under intuitive categories.

### Content Hubs

**Screen (Visual)**
| Hub | Covers |
|---|---|
| Movies | All films — blockbusters, indie, foreign, short films. Documentaries and stand-up specials appear as genre filters here |
| TV Shows | All series — network, streaming, web series, mini-series, limited series. Stand-up specials also filterable here |
| Anime | Japanese animation — separate hub due to distinct community needs, MAL integration, seasonal tracking |
| Cartoons & Animation | Western animation — often excluded from anime trackers |

**Audio**
| Hub | Covers |
|---|---|
| Music Albums | Albums, EPs, singles — listen tracking, ratings, want to listen, discovery |
| Podcasts | Episode-level tracking, subscribe/follow, listening progress |
| Audiobooks | Separate from books — different format, different communities |

**Written**
| Hub | Covers |
|---|---|
| Books | All genres, all formats |
| Manga | Japanese comics — chapter-level tracking |
| Manhwa & Webtoons | Korean/Chinese comics — chapter-level tracking, vertical scroll format |
| Light Novels | Japanese prose — strong overlap with anime community |
| Comic Books | Western comics — issue-level tracking (Marvel, DC, indie, self-published) |
| Graphic Novels | Standalone collected works |

**Gaming**
| Hub | Covers |
|---|---|
| Video Games | Full detailed/simple tracking system, DLC management, achievement tracking, multi-platform |
| Board Games | Session logging, player tracking, win records, BGG integration |
| Tabletop RPGs | Campaign tracking, session logs, character snapshots — tailored for D&D, Pathfinder, etc. |

**Experiences**
| Hub | Covers |
|---|---|
| Restaurants | Reviews, ratings, cuisine tags, visit tracking |
| Bars & Cafes | Separate from restaurants — drink focus, atmosphere notes |
| Events | Concerts, theatre, exhibitions, sports — attended/want to attend |

---

## Core Functionality

### Authentication & Access
- **Authentication wall** — users must register/login to access the service
- Full registration flow with email verification
- Social login (Google, GitHub, Steam)
- Secure session management

### Content Discovery (Per Hub)
- **Smart sorting** — New, Popular, Top Rated, Trending, Upcoming, Recently Released, Coming Soon
- **Advanced filters** — Year, Genre, Rating, Status, Country, Language, Studio/Network/Publisher/Developer
- **Streaming availability** — Where to watch in UK, USA, Germany, and more (Movies/TV)
- **Buy/Rent options** — YouTube, Prime Video, Apple TV, Google Play, Vudu, etc. (Movies/TV)
- **Where to buy games** — Steam, Epic Games, PlayStation Store, Xbox Store, Nintendo eShop, GOG, etc.
- **Real-time search** with instant results
- **Triple-API fallback** system for reliability per content type
- **Manual entry fallback** — users can add content that no API covers

### List Management
- Create unlimited custom lists with subgroups per hub
- Default lists vary by content type:
  - Movies/TV/Anime: Watched, Plan to Watch, Currently Watching
  - Games: Played, Playing, Backlog, Wishlist, Completed
  - Books/Manga/Comics: Read, Reading, Plan to Read
  - Music: Listened, Want to Listen, Favourites
  - Restaurants/Bars: Visited, Want to Visit, Favourites
- Drag & drop reordering
- Progress tracking (episodes watched, chapters read, completion %)
- Personal ratings and notes
- Priority levels for plan-to-watch/backlog items
- Bulk actions, import/export (CSV, JSON)
- List sharing (public/private/friends-only)

### Progress Tracking

**TV Shows & Anime**
- Episode-by-episode tracking with season completion
- Visual progress bars
- Auto-detect next episode
- "Continue Watching" dashboard section
- OVA/Special episode tracking (anime)
- Binge-watch mode

**Manga, Manhwa, Light Novels, Comics**
- Chapter-by-chapter tracking
- Volume tracking
- Visual progress bars
- "Continue Reading" dashboard section

**Music Albums**
- Track-level listened/not listened (optional)
- Album-level listened/want to listen
- Replay counter

**Podcasts**
- Episode-level tracking
- Listening progress within episodes
- Subscribe/follow management

**Books & Audiobooks**
- Page/chapter progress
- Reading speed estimates
- "Currently Reading" section

---

## Video Game Tracking System

### The Problem
Not all games should be tracked the same way:
- **Story-driven games** (RPGs, Adventures): Track main quest, side content, collectibles
- **Multiplayer games** (Fortnite, FIFA): No "completion" — just played or not
- **Roguelikes** (Hades, Dead Cells): Progress is about runs and unlocks
- **Live service games** (Destiny, Warframe): Endless content, no real "finish"

### The Solution: Flexible Tracking Modes

Users choose **Detailed Mode** or **Simple Mode** per game. Auto-suggestions based on genre but user always has control. Can switch modes anytime without losing data.

**Detailed Mode** (for RPGs, story games, open world):
```
[Game Card]
├── Main Story:      [===========75%==----] 75%
├── Side Content:    [=====40%=----------] 40%
├── Full Completion: [====55%=---------]   55%
├── Playtime: 45 hours
├── Milestones: ✅ 8/15 completed
└── Status: Playing
```

**Simple Mode** (for multiplayer, casual, roguelikes):
```
[Game Card]
├── Status: Playing
├── Playtime: 120 hours
└── Last played: 2 days ago
```

### Game Status System
- Not Started, Playing, Beat, Completed, 100%, Played, Paused, Dropped, Endless

### DLC Tracking
- Mark DLC as owned, played, completed
- Individual progress per DLC
- DLC wishlist

### Platform-Specific Tracking
- Track same game on different platforms separately
- Import from Steam, PlayStation, Xbox profiles

---

## Board Game Tracking System

- **Lists** — Owned, Want to Own, Played, Favourites
- **Session logging** — date, players present, who won, duration, notes
- **Per-play rating** — a game feels different at different player counts
- **Play counter** — total times played
- **Player count notes** — "best at 4 players"
- **BGG integration** — covers 150,000+ games including obscure ones

---

## Tabletop RPG Tracking System

Tailored for D&D 5e, Pathfinder 2e, Call of Cthulhu, Shadowrun, Blades in the Dark, Cyberpunk RED, and more.

### Campaign Tracker
- Create campaigns — name, system (D&D 5e, Pathfinder 2e, etc.), players
- Player vs GM mode — GMs see NPC notes and plot threads, players see character progress

### Session Log
- End-of-session input optimised for speed (single screen, big tap targets — people are tired after a 4-hour session)
- Date, duration, players present
- Session notes / recap
- Loot acquired
- Quest updates

### Character Sheet Snapshot
- Name, class, level, HP, brief notes
- Not a full character builder — just the essentials for tracking

### Quest & Objective Tracker
- Simple checklist of active quests
- Mark complete as you progress

### XP / Milestone Tracker
- Level-up tracking and alerts

---

## Restaurant, Bar & Cafe Tracking

- **Lists** — Visited, Want to Visit, Favourites, Avoid
- **Visit logging** — date, who you went with, what you ordered
- **Ratings** — food, service, atmosphere, value (separate scores)
- **Tags** — cuisine type, price range, occasion (date night, casual, business)
- **Photos** — attach photos to visits
- **Revisit tracking** — how many times, favourite orders
- **Location-based** — map view, nearby suggestions

---

## API Integration Strategy

### Triple-Fallback System Per Content Type

Each hub uses at least 3 APIs where possible. If the primary fails (timeout/rate limit/error), Fallback 1 is tried, then Fallback 2. If all fail, cached data is served and a retry is queued.

**Movies**
| Priority | API | Purpose |
|---|---|---|
| Primary | TMDB (The Movie Database) | Free, comprehensive, community-maintained (great for obscure content), streaming providers |
| Fallback 1 | OMDb API | IMDb data, backup metadata |
| Fallback 2 | Trakt.tv API | Community ratings and data |

**TV Shows**
| Priority | API | Purpose |
|---|---|---|
| Primary | TMDB | Metadata, streaming info, episode schedules |
| Fallback 1 | TVmaze API | Episode-level data, excellent for obscure/international shows and web series |
| Fallback 2 | Trakt.tv API | Community data, user ratings |

**Anime**
| Priority | API | Purpose |
|---|---|---|
| Primary | MyAnimeList Official API | Authoritative source, official data, episode schedules, airing status |
| Fallback 1 | AniList API (GraphQL) | Fast, modern, no rate limits, excellent for currently airing schedules |
| Fallback 2 | Kitsu API | Public (no key needed), good supplementary data |
| Optional | Jikan API | Fills gaps the official MAL API doesn't expose (seasonal lists, full schedules) |

**Manga / Manhwa / Light Novels**
| Priority | API | Purpose |
|---|---|---|
| Primary | MangaDex API | Best coverage including extremely obscure works, community-maintained |
| Fallback 1 | MyAnimeList API | Has manga section, same credentials as anime |
| Fallback 2 | AniList API | Also covers manga with great data |

**Books**
| Priority | API | Purpose |
|---|---|---|
| Primary | Open Library API | Open database, near-complete coverage |
| Fallback 1 | Google Books API | Large database, good metadata |

**Comic Books**
| Priority | API | Purpose |
|---|---|---|
| Primary | ComicVine API | Free, massive, includes indie/self-published |

**Video Games**
| Priority | API | Purpose |
|---|---|---|
| Primary | IGDB API (Twitch/Amazon) | Industry-standard, comprehensive |
| Fallback 1 | RAWG API | 500k+ games, great metadata, good for indie/obscure |
| Fallback 2 | Giant Bomb API | Detailed info, good for older/retro games |

**Board Games**
| Priority | API | Purpose |
|---|---|---|
| Primary | BoardGameGeek XML API | Definitive board game database, 150,000+ games |

**Music Albums**
| Priority | API | Purpose |
|---|---|---|
| Primary | MusicBrainz API | Open database, includes very obscure releases |

**Podcasts**
| Priority | API | Purpose |
|---|---|---|
| Primary | Podcast Index API | Open, covers every podcast including tiny independent ones |

**Game Platforms & Stores**
| API | Purpose |
|---|---|
| Steam API | Library import, playtime, achievements |
| PlayStation API | Trophy data, playtime, library |
| Xbox API | Achievements, gamerscore, library |
| HowLongToBeat | Completion time estimates (scraping) |
| IsThereAnyDeal API | Price tracking across stores |

**Streaming Availability**
| API | Purpose |
|---|---|
| TMDB Watch Providers | Free, 100+ countries, streaming/rent/buy options, direct links |
| JustWatch (unofficial) | Fallback, more detailed pricing |

### Data Refresh Intervals

| Content | Status | Refresh Interval | Reason |
|---|---|---|---|
| Anime | Currently airing | Every 24 hours | Breaks, holidays, illness delays are announced within a day |
| Anime | Upcoming (confirmed date) | Every 3 days | Dates rarely change once confirmed |
| Anime | Upcoming (unannounced) | Weekly | Season announcements come in bulk quarterly |
| TV Shows | Currently airing | Every 24 hours | Mid-season breaks, schedule changes, cancellations |
| TV Shows | Upcoming | Every 3 days | Network schedule changes happen but not constantly |
| Movies | Upcoming (< 1 month) | Every 3 days | Last-minute delays still happen |
| Movies | Upcoming (> 1 month) | Weekly | Release dates this far out rarely shift more than once a week |
| Movies | Released | Monthly | Streaming availability updates |
| Manga | Ongoing | Weekly | Most manga releases weekly |
| Games | Upcoming | Every 3 days | Publisher delays are common |
| Games | Released | Weekly | DLC/patch info, sale prices |
| Music | New releases | Weekly | Album drops are typically announced well ahead |
| Podcasts | Active shows | Daily | New episodes drop frequently |

---

## Streaming & Purchase Availability

### Where to Watch (Movies / TV / Anime)
- Multi-country support: UK, USA, Germany, Canada, Australia, France, Japan, and more
- Streaming platforms: Netflix, Disney+, Hulu, HBO Max, Apple TV+, Amazon Prime, Crunchyroll, etc.
- Buy options: iTunes, Google Play, YouTube, Microsoft Store, Vudu
- Rent options: Prime Video, YouTube, Google Play, Apple TV
- Auto-updated daily via background jobs
- Pricing info where available
- Direct links to watch
- User selects preferred country in settings

### Where to Buy (Games)
- Steam, Epic Games, PlayStation Store, Xbox Store, Nintendo eShop, GOG
- Price comparison across stores
- Sale alerts for wishlisted games
- Price history

---

## Tech Stack

### Backend
- **Laravel 10+** — modern PHP framework
- **PostgreSQL 16+** — relational data with JSONB support, superior indexing, and full-text search
- **Redis** — caching layer for API responses and sessions
- **Laravel Horizon** — queue monitoring and management
- **Docker** — containerised deployment with independent worker containers per content type

### Frontend
- **Vue 3 (Composition API)** — lightweight, fast, excellent Laravel integration
- **Inertia.js** — SPA experience without API overhead
- **Vite** — build tool
- **Tailwind CSS** — utility-first CSS
- **Pinia** — state management

### Why Vue Over React
- Vue 3 bundle is ~30% smaller than React
- First-class Laravel support via Inertia.js/Breeze
- Composition API is comparable to React Hooks
- Built-in reactivity — no extra libraries needed
- Performance difference is negligible; integration is superior

---

## Performance Optimisations

- **Lazy loading** — images and components loaded on-demand
- **Virtual scrolling** — 60fps for long lists (vue-virtual-scroller)
- **Debounced search** — 300ms, reduces API calls
- **Aggressive caching** — Redis for API responses (TTL: 1–24 hours based on content type)
- **Queue system** — background jobs for API calls, updates, notifications
- **Database indexing** — optimised queries with compound indexes
- **CDN** — static assets and images
- **Cursor-based pagination** — for infinite scroll
- **Route-based code splitting** — smaller initial bundle
- **Image CDN** — WebP/AVIF with blur-up progressive loading
- **Service worker** — offline capabilities (PWA)
- **Optimistic UI updates** — instant feedback before server confirms
- **Loading skeletons** — no blank screens
- **Prefetching on hover** — anticipate navigation

### Performance Targets
| Metric | Target |
|---|---|
| First Contentful Paint | < 1.5s |
| Route Transition | < 200ms |
| List View Render | < 500ms |
| Search Results | < 800ms |
| API Response (cached) | < 50ms |
| API Response (uncached) | < 2s |
| Database Queries | < 100ms |
| Time to Interactive | < 3s |
| Infinite Scroll | 60fps |

---

## Complete Feature Set

### Authentication & User Management
- Mandatory login/registration
- Email/password authentication
- Social OAuth (Google, GitHub)
- Email verification
- Password reset flow
- Profile customisation (avatar, bio, timezone)
- Privacy settings (public/private lists)
- Account deletion with data export

### Advanced Filters

**Media (Movies / TV / Anime / Cartoons)**
- Year/Date Range, Genres (multi-select), Minimum Rating, Status (Released/Airing/Ended/Upcoming/Cancelled)
- Country, Language, Studio/Network, Runtime, Popularity, Content Rating (G, PG, PG-13, R, TV-MA)

**Written (Books / Manga / Comics)**
- Year, Genre, Author/Artist, Rating, Status (Ongoing/Completed/Hiatus), Publisher, Language

**Games**
- Year, Genres, Rating, Status (Released/Early Access/Upcoming/Beta)
- Platforms (PC, PlayStation, Xbox, Switch, Mobile), Developer/Publisher
- Player Modes (Single-player, Multiplayer, Co-op, MMO)
- Average Playtime, ESRB Rating, Features (Achievements, Controller, VR)

**Music**
- Year, Genre, Artist, Label, Rating

**Podcasts**
- Genre/Category, Language, Active/Ended, Episode Count

### Personal Notes & Ratings
- Personal rating (0–10 or 5-star)
- Private notes and reviews
- Date watched/played/read/listened/added
- Custom tags (e.g. "mind-bending", "tearjerker", "couch co-op")
- Priority levels (high/medium/low for backlog items)
- Favourite marking
- Platform-specific notes for games

### Smart Features
- **Random Picker** — can't decide? Pick random from your lists, filter by mood/genre/length/platform
- **Smart Notifications** — new episodes, streaming availability changes, game sales, friend activity
- **Statistics Dashboard** — total time across all media types, genre breakdowns, year-by-year, completion rates
- **Calendar View** — upcoming episodes, releases, game launches
- **Advanced Search** — by cast, director, developer, keywords, "similar to X"
- **AI Recommendations** — ML-based suggestions based on taste across all media types
- **PWA Support** — install as mobile app, offline access to lists
- **Dark/Light/Auto Theme** — system-aware
- **Keyboard Shortcuts** — power user navigation
- **Import from Other Services** — IMDb, Trakt, MyAnimeList, AniList, Steam, PlayStation, Xbox, GOG, Goodreads
- **Export Data** — GDPR-compliant data export (CSV, JSON)

### Social Features
- Friends system with activity feed
- Taste match compatibility scores
- Comments on friends' lists and activity
- Achievements/badges (gamification)
- Shared/collaborative lists
- Activity feed ("X just finished Y")

### Discovery Features
- Similar content recommendations
- Mood-based discovery
- Trending in your network
- Hidden gems (highly rated but under-tracked)
- Game-specific discovery (similar by mechanics, "great for couch co-op", "perfect for Steam Deck")

### Convenience Features
- **Time Estimator** — hours to finish a series, beat your backlog, HowLongToBeat integration
- **Backlog Calculator** — "At 10hrs/week, you'll finish your backlog in 3.5 months"
- **Quick Add** — browser extension
- **Voice Input** — "Add Breaking Bad to my plan to watch list"
- **Email Digests** — weekly summary of new content and game sales
- **List Templates** — Oscar Winners, MCU Order, Top 100 IMDb, Must-Play Indies, FromSoftware Catalog
- **Sync Across Devices** — real-time
- **Price Tracking** — alert when wishlisted games go on sale

---

## Database Schema

```sql
-- PostgreSQL with JSONB columns for flexible metadata
-- All JSON fields use JSONB (indexable, queryable)

-- Users & Authentication
users
- id, name, email, email_verified_at, password, avatar, bio, timezone
- country_code, language, theme (dark/light/auto)
- settings (JSON: notifications, privacy, display preferences)
- last_active_at, created_at, updated_at

social_logins
- id, user_id, provider (google/github/steam), provider_id, token, refresh_token

-- Universal Content Table
media_items
- id, media_type ENUM (movie/show/anime/cartoon/manga/manhwa/light_novel/book/
  comic/graphic_novel/game/board_game/ttrpg/music_album/podcast/audiobook)
- external_id, tmdb_id, imdb_id, mal_id, igdb_id, steam_id, anilist_id,
  mangadex_id, bgg_id, musicbrainz_id, openlibrary_id, comicvine_id
- title, original_title, slug, year, release_date
- poster_url, backdrop_url, trailer_url
- overview (text), genres (JSON), status
- rating (decimal), vote_count, popularity
- creator (JSON: director/author/artist/developer/studio)
- country, language
- total_episodes, total_seasons, total_chapters, total_volumes
- runtime_minutes
- data (JSON: additional type-specific metadata)
- last_synced_at, created_at, updated_at
- INDEXES: media_type, external_id, slug, year, rating, popularity
- GIN INDEX: genres (JSONB), to_tsvector(title || overview)

-- Games Extended Data
games_extended
- id, media_item_id
- developer, publisher, engine
- platforms (JSON)
- player_modes (JSON)
- esrb_rating, pegi_rating
- hltb_main_story, hltb_main_extras, hltb_completionist (hours)
- metacritic_score, opencritic_score
- has_achievements, achievement_count
- has_multiplayer, has_coop, max_players
- supports_controller, supports_vr, has_cloud_saves
- franchise, series_order
- data (JSON: system requirements, languages)

-- Game DLCs & Expansions
game_dlcs
- id, game_id, external_dlc_id
- name, slug, type (dlc/expansion/season_pass)
- release_date, price, description, poster_url
- hltb_hours

-- Game Prices (Auto-updated)
game_prices
- id, media_item_id, platform_store (steam/epic/psn/xbox/gog)
- country_code, price, currency, discount_percent, sale_ends_at, url

-- Board Game Extended Data
board_games_extended
- id, media_item_id
- bgg_id, min_players, max_players, best_player_count
- playing_time_minutes, min_age
- weight_rating (complexity 1-5)
- categories (JSON), mechanics (JSON)
- designer, artist, publisher

-- Board Game Sessions
board_game_sessions
- id, user_id, media_item_id
- played_at, duration_minutes
- player_count, players (JSON: names/user_ids)
- winner (nullable), notes
- personal_rating

-- TTRPG Campaigns
ttrpg_campaigns
- id, user_id, media_item_id (the game system e.g. D&D 5e)
- name, description, status (active/paused/completed/abandoned)
- role ENUM (player/gm)
- system_name, system_edition
- created_at, updated_at

-- TTRPG Characters (snapshot, not a full builder)
ttrpg_characters
- id, campaign_id, user_id
- name, class, level, race
- hp_current, hp_max
- notes (text), data (JSON: key stats)
- created_at, updated_at

-- TTRPG Sessions
ttrpg_sessions
- id, campaign_id
- session_number, played_at, duration_minutes
- players_present (JSON)
- recap (text), notes (text)
- loot (JSON), quests_updated (JSON)
- xp_gained, milestones (JSON)

-- Streaming Availability
streaming_availability
- id, media_item_id, country_code
- platform_type (streaming/rent/buy)
- provider_name, provider_logo_url, provider_url
- price (decimal, nullable), currency (nullable)
- quality (SD/HD/4K, nullable)
- updated_at

-- Restaurant / Bar / Cafe Reviews
venue_reviews
- id, user_id
- name, venue_type ENUM (restaurant/bar/cafe)
- location, address, latitude, longitude
- cuisine_tags (JSON), price_range (1-4)
- overall_rating, food_rating, service_rating, atmosphere_rating, value_rating
- notes (text), photos (JSON)
- visited_at, revisit_count
- is_favourite
- created_at, updated_at

-- Lists & Organisation
lists
- id, user_id, name, slug
- type (watched/plan_to_watch/currently_watching/read/reading/
  plan_to_read/played/playing/backlog/wishlist/completed/
  listened/want_to_listen/visited/want_to_visit/custom)
- media_type_scope (nullable — restrict list to one content type, or null for mixed)
- description, is_public, is_collaborative
- position, color, icon
- created_at, updated_at

list_subgroups
- id, list_id, name, position, color

list_items
- id, list_id, subgroup_id (nullable), media_item_id, user_id
- position, status, personal_rating (0-10), priority (high/medium/low)
- notes (text), tags (JSON)
- is_favourite, rewatch_count
- date_added, date_started, date_completed

-- Watch/Read Progress (TV/Anime/Manga/Comics)
episode_progress
- id, user_id, media_item_id
- season_number (nullable), episode_number (or chapter_number)
- watched (boolean), watch_date
- UNIQUE: user_id + media_item_id + season_number + episode_number

season_progress
- id, user_id, media_item_id, season_number (or volume_number)
- total_episodes, episodes_watched, completed

-- Game Progress
game_progress
- id, user_id, media_item_id, platform
- tracking_mode ENUM (detailed/simple)
- status ENUM (not_started/playing/beat/completed/100_percent/played/paused/dropped/endless)
- playtime_hours (decimal)
- main_story_percentage (nullable), side_content_percentage (nullable),
  full_completion_percentage (nullable)
- milestones_completed (JSON, nullable), custom_goals (JSON, nullable)
- is_played (boolean)
- achievement_count, achievements_unlocked
- first_played_at, last_played_at
- is_replay, replay_count, notes (text)
- UNIQUE: user_id + media_item_id + platform

game_play_sessions
- id, user_id, game_progress_id
- session_start, session_end, duration_minutes, notes

game_dlc_progress
- id, user_id, game_dlc_id
- owned, completed, playtime_hours, completion_percentage, started_at, completed_at

-- Reading Progress (Books/Audiobooks)
reading_progress
- id, user_id, media_item_id
- current_page (nullable), total_pages (nullable)
- current_chapter (nullable), total_chapters (nullable)
- percentage, status (not_started/reading/completed/paused/dropped)
- started_at, completed_at

-- Music Listening Progress
listening_progress
- id, user_id, media_item_id
- status (not_listened/listening/listened/want_to_listen)
- listen_count, personal_rating
- date_first_listened, date_last_listened, notes (text)

-- Podcast Progress
podcast_progress
- id, user_id, media_item_id
- subscribed (boolean)
- episodes_listened, total_episodes
- last_episode_number, last_listened_at

-- Social Features
friendships
- id, user_id, friend_id, status (pending/accepted/blocked)

activities
- id, user_id, activity_type, media_item_id, list_id (nullable)
- data (JSON), is_public, created_at

comments
- id, user_id, commentable_type, commentable_id, content (text)

achievements
- id, user_id, achievement_type, achievement_data (JSON), unlocked_at

-- Recommendations
recommendations
- id, user_id, media_item_id, score, reason (JSON), dismissed

-- Notifications (Laravel default table)
notifications
- id, type, notifiable_type, notifiable_id, data (JSON), read_at

-- API Cache
api_cache
- id, cache_key (unique), provider, endpoint
- response_data (JSON), hit_count, expires_at
```

---

## Required Packages

### Backend (Composer)
```json
{
  "laravel/framework": "^10.0",
  "laravel/breeze": "^1.0",
  "inertiajs/inertia-laravel": "^0.6",
  "guzzlehttp/guzzle": "^7.8",
  "predis/predis": "^2.2",
  "laravel/horizon": "^5.0",
  "laravel/socialite": "^5.10",
  "spatie/laravel-query-builder": "^5.0",
  "spatie/laravel-sluggable": "^3.6",
  "spatie/laravel-backup": "^8.0",
  "intervention/image": "^2.7",
  "meilisearch/meilisearch-php": "^1.0",
  "laravel/scout": "^10.0",
  "pusher/pusher-php-server": "^7.2"
}
```

### Frontend (NPM)
```json
{
  "@inertiajs/vue3": "^1.0",
  "vue": "^3.3",
  "pinia": "^2.1",
  "@vueuse/core": "^10.0",
  "@vueuse/motion": "^2.0",
  "vue-virtual-scroller": "^2.0",
  "tailwindcss": "^3.3",
  "@headlessui/vue": "^1.7",
  "@heroicons/vue": "^2.0",
  "axios": "^1.6",
  "vue-draggable-plus": "^0.3",
  "chart.js": "^4.4",
  "vue-chartjs": "^5.3",
  "date-fns": "^2.30",
  "fuse.js": "^7.0",
  "vite-plugin-pwa": "^0.17",
  "workbox-window": "^7.0",
  "notivue": "^2.0"
}
```

---

## Project Structure

```
/
├── app/
│   ├── Http/
│   │   ├── Controllers/
│   │   │   ├── Auth/
│   │   │   │   ├── RegisterController.php
│   │   │   │   ├── LoginController.php
│   │   │   │   └── SocialAuthController.php
│   │   │   ├── Dashboard/
│   │   │   │   ├── DashboardController.php
│   │   │   │   └── StatsController.php
│   │   │   ├── Media/
│   │   │   │   ├── MovieController.php
│   │   │   │   ├── TvShowController.php
│   │   │   │   ├── AnimeController.php
│   │   │   │   ├── CartoonController.php
│   │   │   │   ├── StreamingAvailabilityController.php
│   │   │   │   └── MediaDetailController.php
│   │   │   ├── Written/
│   │   │   │   ├── BookController.php
│   │   │   │   ├── MangaController.php
│   │   │   │   ├── ManhwaController.php
│   │   │   │   ├── LightNovelController.php
│   │   │   │   ├── ComicBookController.php
│   │   │   │   └── GraphicNovelController.php
│   │   │   ├── Gaming/
│   │   │   │   ├── GameController.php
│   │   │   │   ├── GameProgressController.php
│   │   │   │   ├── DLCController.php
│   │   │   │   ├── GamePriceController.php
│   │   │   │   ├── AchievementController.php
│   │   │   │   ├── BoardGameController.php
│   │   │   │   ├── BoardGameSessionController.php
│   │   │   │   ├── TtrpgCampaignController.php
│   │   │   │   └── TtrpgSessionController.php
│   │   │   ├── Audio/
│   │   │   │   ├── MusicAlbumController.php
│   │   │   │   ├── PodcastController.php
│   │   │   │   └── AudiobookController.php
│   │   │   ├── Experiences/
│   │   │   │   ├── VenueController.php
│   │   │   │   └── EventController.php
│   │   │   ├── Search/
│   │   │   │   ├── SearchController.php
│   │   │   │   └── DiscoverController.php
│   │   │   ├── Lists/
│   │   │   │   ├── ListController.php
│   │   │   │   ├── ListItemController.php
│   │   │   │   ├── SubgroupController.php
│   │   │   │   └── ListShareController.php
│   │   │   ├── Progress/
│   │   │   │   ├── EpisodeProgressController.php
│   │   │   │   ├── ReadingProgressController.php
│   │   │   │   ├── ListeningProgressController.php
│   │   │   │   └── PodcastProgressController.php
│   │   │   ├── Social/
│   │   │   │   ├── FriendController.php
│   │   │   │   ├── ActivityController.php
│   │   │   │   └── CommentController.php
│   │   │   └── User/
│   │   │       ├── ProfileController.php
│   │   │       ├── SettingsController.php
│   │   │       └── NotificationController.php
│   │   └── Middleware/
│   │       ├── MustBeAuthenticated.php
│   │       └── TrackActivity.php
│   │
│   ├── Models/
│   │   ├── User.php
│   │   ├── SocialLogin.php
│   │   ├── MediaItem.php
│   │   ├── GamesExtended.php
│   │   ├── GameDlc.php
│   │   ├── GamePrice.php
│   │   ├── BoardGamesExtended.php
│   │   ├── BoardGameSession.php
│   │   ├── TtrpgCampaign.php
│   │   ├── TtrpgCharacter.php
│   │   ├── TtrpgSession.php
│   │   ├── StreamingAvailability.php
│   │   ├── VenueReview.php
│   │   ├── MediaList.php
│   │   ├── ListSubgroup.php
│   │   ├── ListItem.php
│   │   ├── EpisodeProgress.php
│   │   ├── SeasonProgress.php
│   │   ├── GameProgress.php
│   │   ├── GamePlaySession.php
│   │   ├── GameDlcProgress.php
│   │   ├── ReadingProgress.php
│   │   ├── ListeningProgress.php
│   │   ├── PodcastProgress.php
│   │   ├── Friendship.php
│   │   ├── Activity.php
│   │   ├── Comment.php
│   │   ├── Achievement.php
│   │   ├── Recommendation.php
│   │   └── ApiCache.php
│   │
│   ├── Services/
│   │   ├── MediaApiService.php
│   │   ├── CacheService.php
│   │   ├── RecommendationEngine.php
│   │   ├── NotificationService.php
│   │   ├── StatisticsService.php
│   │   └── ApiProviders/
│   │       ├── Contracts/
│   │       │   └── MediaProviderInterface.php
│   │       ├── Movies/
│   │       │   ├── TmdbMovieProvider.php
│   │       │   ├── OmdbProvider.php
│   │       │   └── TraktMovieProvider.php
│   │       ├── TvShows/
│   │       │   ├── TmdbTvProvider.php
│   │       │   ├── TvMazeProvider.php
│   │       │   └── TraktTvProvider.php
│   │       ├── Anime/
│   │       │   ├── MyAnimeListProvider.php
│   │       │   ├── AniListProvider.php
│   │       │   ├── KitsuProvider.php
│   │       │   └── JikanProvider.php
│   │       ├── Written/
│   │       │   ├── MangaDexProvider.php
│   │       │   ├── OpenLibraryProvider.php
│   │       │   ├── GoogleBooksProvider.php
│   │       │   └── ComicVineProvider.php
│   │       ├── Games/
│   │       │   ├── IgdbProvider.php
│   │       │   ├── RawgProvider.php
│   │       │   ├── GiantBombProvider.php
│   │       │   ├── SteamProvider.php
│   │       │   ├── HowLongToBeatScraper.php
│   │       │   └── IsThereAnyDealProvider.php
│   │       ├── BoardGames/
│   │       │   └── BggProvider.php
│   │       ├── Audio/
│   │       │   ├── MusicBrainzProvider.php
│   │       │   └── PodcastIndexProvider.php
│   │       └── Streaming/
│   │           ├── TmdbWatchProviderService.php
│   │           └── JustWatchProvider.php
│   │
│   ├── Jobs/
│   │   ├── Media/
│   │   │   ├── SyncMediaData.php
│   │   │   ├── UpdatePopularContent.php
│   │   │   └── RefreshStreamingAvailability.php
│   │   ├── Games/
│   │   │   ├── SyncGameData.php
│   │   │   ├── UpdateGamePrices.php
│   │   │   ├── CheckGameSales.php
│   │   │   ├── SyncSteamLibrary.php
│   │   │   └── UpdateHLTBData.php
│   │   ├── Written/
│   │   │   ├── SyncMangaChapters.php
│   │   │   └── SyncBookData.php
│   │   ├── Audio/
│   │   │   ├── SyncMusicData.php
│   │   │   └── SyncPodcastEpisodes.php
│   │   ├── Notifications/
│   │   │   ├── NotifyNewEpisode.php
│   │   │   ├── NotifyNewChapter.php
│   │   │   ├── NotifyStreamingAvailable.php
│   │   │   ├── NotifyGameOnSale.php
│   │   │   └── NotifyFriendActivity.php
│   │   └── User/
│   │       ├── SendWeeklyDigest.php
│   │       └── CalculateStatistics.php
│   │
│   └── Console/
│       └── Commands/
│           ├── RefreshPopularContent.php
│           ├── RefreshAiringContent.php
│           ├── CleanOldCache.php
│           └── UpdateStreamingAvailability.php
│
├── resources/
│   ├── js/
│   │   ├── Pages/
│   │   │   ├── Auth/
│   │   │   │   ├── Login.vue
│   │   │   │   ├── Register.vue
│   │   │   │   └── ForgotPassword.vue
│   │   │   ├── Dashboard.vue
│   │   │   ├── Movies/
│   │   │   │   ├── Index.vue
│   │   │   │   └── Show.vue
│   │   │   ├── TvShows/
│   │   │   │   ├── Index.vue
│   │   │   │   └── Show.vue
│   │   │   ├── Anime/
│   │   │   │   ├── Index.vue
│   │   │   │   └── Show.vue
│   │   │   ├── Cartoons/
│   │   │   │   ├── Index.vue
│   │   │   │   └── Show.vue
│   │   │   ├── Books/
│   │   │   │   ├── Index.vue
│   │   │   │   └── Show.vue
│   │   │   ├── Manga/
│   │   │   │   ├── Index.vue
│   │   │   │   └── Show.vue
│   │   │   ├── Manhwa/
│   │   │   │   ├── Index.vue
│   │   │   │   └── Show.vue
│   │   │   ├── LightNovels/
│   │   │   │   ├── Index.vue
│   │   │   │   └── Show.vue
│   │   │   ├── Comics/
│   │   │   │   ├── Index.vue
│   │   │   │   └── Show.vue
│   │   │   ├── Games/
│   │   │   │   ├── Index.vue
│   │   │   │   ├── Show.vue
│   │   │   │   └── DLCManager.vue
│   │   │   ├── BoardGames/
│   │   │   │   ├── Index.vue
│   │   │   │   ├── Show.vue
│   │   │   │   └── SessionLog.vue
│   │   │   ├── Ttrpg/
│   │   │   │   ├── Campaigns.vue
│   │   │   │   ├── CampaignShow.vue
│   │   │   │   ├── SessionLog.vue
│   │   │   │   └── CharacterSheet.vue
│   │   │   ├── Music/
│   │   │   │   ├── Index.vue
│   │   │   │   └── Show.vue
│   │   │   ├── Podcasts/
│   │   │   │   ├── Index.vue
│   │   │   │   └── Show.vue
│   │   │   ├── Audiobooks/
│   │   │   │   ├── Index.vue
│   │   │   │   └── Show.vue
│   │   │   ├── Venues/
│   │   │   │   ├── Index.vue
│   │   │   │   └── Show.vue
│   │   │   ├── Events/
│   │   │   │   ├── Index.vue
│   │   │   │   └── Show.vue
│   │   │   ├── Lists/
│   │   │   │   ├── Index.vue
│   │   │   │   ├── Show.vue
│   │   │   │   └── Shared.vue
│   │   │   ├── Search/
│   │   │   │   └── Index.vue
│   │   │   ├── Social/
│   │   │   │   ├── Friends.vue
│   │   │   │   ├── Activity.vue
│   │   │   │   └── Profile.vue
│   │   │   ├── Stats/
│   │   │   │   └── Index.vue
│   │   │   ├── Calendar/
│   │   │   │   └── Index.vue
│   │   │   └── Profile/
│   │   │       ├── Show.vue
│   │   │       └── Settings.vue
│   │   │
│   │   ├── Components/
│   │   │   ├── Layout/
│   │   │   │   ├── AppLayout.vue
│   │   │   │   ├── Navigation.vue
│   │   │   │   ├── Sidebar.vue
│   │   │   │   └── Footer.vue
│   │   │   ├── Media/
│   │   │   │   ├── MediaCard.vue
│   │   │   │   ├── MediaGrid.vue
│   │   │   │   ├── MediaDetails.vue
│   │   │   │   ├── StreamingBadges.vue
│   │   │   │   ├── EpisodeList.vue
│   │   │   │   ├── ChapterList.vue
│   │   │   │   ├── ProgressBar.vue
│   │   │   │   └── TrailerPlayer.vue
│   │   │   ├── Gaming/
│   │   │   │   ├── GameCard.vue
│   │   │   │   ├── TrackingModeSelector.vue
│   │   │   │   ├── BoardGameSessionForm.vue
│   │   │   │   ├── CampaignCard.vue
│   │   │   │   ├── SessionLogForm.vue
│   │   │   │   └── CharacterSnapshot.vue
│   │   │   ├── Lists/
│   │   │   │   ├── ListManager.vue
│   │   │   │   ├── ListCard.vue
│   │   │   │   ├── DraggableList.vue
│   │   │   │   └── QuickAddButton.vue
│   │   │   ├── Search/
│   │   │   │   ├── SearchBar.vue
│   │   │   │   ├── AdvancedFilters.vue
│   │   │   │   └── SearchResults.vue
│   │   │   ├── Social/
│   │   │   │   ├── ActivityFeed.vue
│   │   │   │   ├── FriendCard.vue
│   │   │   │   └── TasteMatch.vue
│   │   │   ├── Stats/
│   │   │   │   ├── StatsCard.vue
│   │   │   │   ├── GenreChart.vue
│   │   │   │   └── TimeChart.vue
│   │   │   └── UI/
│   │   │       ├── Button.vue
│   │   │       ├── Modal.vue
│   │   │       ├── Dropdown.vue
│   │   │       ├── Tabs.vue
│   │   │       ├── Badge.vue
│   │   │       ├── LoadingSkeleton.vue
│   │   │       └── Toast.vue
│   │   │
│   │   ├── Composables/
│   │   │   ├── useMediaSearch.js
│   │   │   ├── useListManager.js
│   │   │   ├── useInfiniteScroll.js
│   │   │   ├── useProgress.js
│   │   │   ├── useDragAndDrop.js
│   │   │   ├── useNotifications.js
│   │   │   ├── useAuth.js
│   │   │   └── useFilters.js
│   │   │
│   │   ├── Stores/
│   │   │   ├── auth.js
│   │   │   ├── media.js
│   │   │   ├── lists.js
│   │   │   ├── notifications.js
│   │   │   └── ui.js
│   │   │
│   │   ├── Utils/
│   │   │   ├── api.js
│   │   │   ├── formatters.js
│   │   │   ├── validators.js
│   │   │   └── constants.js
│   │   │
│   │   └── app.js
│   │
│   └── css/
│       └── app.css
│
├── routes/
│   ├── web.php
│   ├── auth.php
│   └── api.php
│
├── config/
│   ├── services.php
│   ├── horizon.php
│   └── scout.php
│
└── public/
    ├── service-worker.js
    └── manifest.json
```

---

## Environment Variables

```env
APP_NAME="OmniTrakr"
APP_ENV=production
APP_DEBUG=false
APP_URL=https://omnitrakr.com

# Database
DB_CONNECTION=pgsql
DB_HOST=postgres
DB_PORT=5432
DB_DATABASE=omnitrakr
DB_USERNAME=omnitrakr
DB_PASSWORD=

# Redis
REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379
CACHE_DRIVER=redis
SESSION_DRIVER=redis
QUEUE_CONNECTION=redis

# Content APIs — Movies/TV
TMDB_API_KEY=
TMDB_API_TOKEN=
OMDB_API_KEY=
TRAKT_CLIENT_ID=
TRAKT_CLIENT_SECRET=

# Anime APIs
MYANIMELIST_CLIENT_ID=
MYANIMELIST_CLIENT_SECRET=
ANILIST_CLIENT_ID=

# Written Content APIs
MANGADEX_API_KEY=
GOOGLE_BOOKS_API_KEY=
COMICVINE_API_KEY=

# Game APIs
IGDB_CLIENT_ID=
IGDB_CLIENT_SECRET=
RAWG_API_KEY=
GIANTBOMB_API_KEY=
STEAM_API_KEY=
ISTHEREANYDEAL_API_KEY=

# Audio APIs
MUSICBRAINZ_USER_AGENT=OmniTrakr/1.0
PODCAST_INDEX_API_KEY=
PODCAST_INDEX_API_SECRET=

# Social Login
GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=
GOOGLE_REDIRECT_URL="${APP_URL}/auth/google/callback"

GITHUB_CLIENT_ID=
GITHUB_CLIENT_SECRET=
GITHUB_REDIRECT_URL="${APP_URL}/auth/github/callback"

STEAM_LOGIN_API_KEY=

# Email
MAIL_MAILER=smtp
MAIL_HOST=
MAIL_PORT=587
MAIL_USERNAME=
MAIL_PASSWORD=
MAIL_ENCRYPTION=tls
MAIL_FROM_ADDRESS="noreply@omnitrakr.com"
MAIL_FROM_NAME="${APP_NAME}"

# Queue & Background Jobs
HORIZON_ENABLED=true
HORIZON_MEMORY_LIMIT=256

# Search
SCOUT_DRIVER=meilisearch
MEILISEARCH_HOST=http://127.0.0.1:7700
MEILISEARCH_KEY=

# Real-time Notifications
BROADCAST_DRIVER=pusher
PUSHER_APP_ID=
PUSHER_APP_KEY=
PUSHER_APP_SECRET=
PUSHER_APP_CLUSTER=mt1
```

---

## API Keys to Obtain (All Free Tier)

| API | URL | Free Tier |
|---|---|---|
| TMDB | https://www.themoviedb.org/settings/api | Unlimited requests |
| OMDb | http://www.omdbapi.com/apikey.aspx | 1,000 requests/day |
| Trakt.tv | https://trakt.tv/oauth/applications | Free tier available |
| MyAnimeList | https://myanimelist.net/apiconfig | Official API, create app for credentials |
| AniList | https://anilist.co/settings/developer | GraphQL, no rate limits |
| Kitsu | https://kitsu.docs.apiary.io | No key needed (public) |
| MangaDex | https://api.mangadex.org/docs | Free, community-maintained |
| Open Library | https://openlibrary.org/developers/api | No key needed |
| Google Books | https://developers.google.com/books | Free tier available |
| ComicVine | https://comicvine.gamespot.com/api | Free tier available |
| IGDB | https://api-docs.igdb.com | 4 requests/second (Twitch dev account) |
| RAWG | https://rawg.io/apidocs | 20,000 requests/month |
| Giant Bomb | https://www.giantbomb.com/api | Free tier available |
| Steam | https://steamcommunity.com/dev/apikey | No limits |
| BoardGameGeek | https://boardgamegeek.com/wiki/page/BGG_XML_API2 | Free XML API |
| MusicBrainz | https://musicbrainz.org/doc/MusicBrainz_API | Free, requires user-agent |
| Podcast Index | https://podcastindex.org | Free, open API |
| IsThereAnyDeal | https://isthereanydeal.com/dev/app | Free for non-commercial |

---

## System Requirements

- PHP 8.2+
- Composer 2.5+
- Node.js 18+ (LTS)
- PostgreSQL 16+
- Redis 7.0+
- Docker & Docker Compose
- Nginx (reverse proxy, handled via Docker)

---

## Implementation Roadmap

### Phase 1: Foundation & Setup (Week 1)
- [ ] Install Laravel 10 with Breeze (Inertia + Vue 3)
- [ ] Configure PostgreSQL with proper charset
- [ ] Install and configure Redis
- [ ] Set up Horizon for queue monitoring
- [ ] Create all database migrations
- [ ] Set up authentication with email verification
- [ ] Configure social login (Google, GitHub)
- [ ] Set up Tailwind CSS with custom config
- [ ] Create base layout components
- [ ] Implement dark/light theme system

### Phase 2: API Integration Layer (Week 2)
- [ ] Build MediaApiService orchestrator with fallback logic
- [ ] Implement TMDB provider (movies + TV + streaming)
- [ ] Implement OMDb and Trakt providers (fallbacks)
- [ ] Implement MyAnimeList, AniList, Kitsu providers
- [ ] Implement MangaDex, Open Library, Google Books, ComicVine providers
- [ ] Implement IGDB, RAWG, Giant Bomb providers
- [ ] Implement BGG provider for board games
- [ ] Implement MusicBrainz and Podcast Index providers
- [ ] Create CacheService with Redis
- [ ] Set up queue jobs for API calls
- [ ] Test all API integrations

### Phase 3: Core Data Models (Week 3)
- [ ] Create all models with relationships
- [ ] Set up model factories for testing
- [ ] Create model observers for events
- [ ] Add database indexes for performance
- [ ] Implement soft deletes where needed

### Phase 4: Screen Hub — Movies, TV, Anime, Cartoons (Week 4)
- [ ] Browse pages with filters and sorting for each
- [ ] Detail pages with full metadata
- [ ] Streaming availability by country
- [ ] Episode tracking UI for TV/Anime
- [ ] Infinite scroll with cursor pagination
- [ ] Search with debouncing

### Phase 5: Written Hub — Books, Manga, Comics (Week 5)
- [ ] Browse pages for Books, Manga, Manhwa, Light Novels, Comics
- [ ] Chapter/volume tracking UI
- [ ] Reading progress system
- [ ] Detail pages

### Phase 6: Gaming Hub — Video Games, Board Games, TTRPGs (Week 6)
- [ ] Video game browse, detail, DLC management
- [ ] Game tracking mode selector (Detailed vs Simple)
- [ ] Board game browse and session logging UI
- [ ] TTRPG campaign tracker, session log, character sheet snapshot
- [ ] End-of-session quick input (single screen, big tap targets)
- [ ] Game price comparison and sale alerts

### Phase 7: Audio Hub — Music, Podcasts, Audiobooks (Week 7)
- [ ] Music album browse and listening tracking
- [ ] Podcast browse and episode tracking
- [ ] Audiobook browse and progress tracking
- [ ] Discovery features per type

### Phase 8: List Management System (Week 8)
- [ ] Default lists per content type
- [ ] Custom list creation with subgroups
- [ ] Drag & drop reordering
- [ ] Quick add button on all cards
- [ ] Bulk actions, import/export
- [ ] List sharing

### Phase 9: Experiences Hub & Social (Week 9)
- [ ] Restaurant/bar/cafe review system
- [ ] Event tracking
- [ ] Friend system and activity feed
- [ ] Taste match algorithm
- [ ] Notifications (real-time via Pusher)
- [ ] Achievement system

### Phase 10: Advanced Features (Week 10)
- [ ] Unified statistics dashboard across all hubs
- [ ] Calendar view (upcoming releases across all content)
- [ ] Random picker with filters
- [ ] Import from external services (IMDb, Trakt, MAL, Steam, Goodreads)
- [ ] Recommendation engine
- [ ] PWA functionality
- [ ] Email digests
- [ ] Keyboard shortcuts
- [ ] Performance optimisation pass

---

## MVP (First Release)

**Must have:**
- Authentication (register/login)
- Browse Movies, TV Shows, Anime with sorting and filters
- Browse Games with sorting and filters
- Search functionality
- Default lists (Watched, Plan to Watch, Playing, Backlog, etc.)
- Episode tracking for TV/Anime
- Game tracking mode selection (Detailed vs Simple)
- Streaming availability (TMDB)
- Personal ratings and notes
- Basic statistics
- Responsive design + dark mode

**Phase 2 (can wait):**
- Written hub (Books, Manga, Comics)
- Audio hub (Music, Podcasts)
- Board games and TTRPG tracking
- Experiences hub (Restaurants, Events)
- Social features
- Advanced recommendations
- Import from external services
- PWA

---

## Branding

**Name:** OmniTrakr

**Style:** The **KR** is capitalised and treated as the standout branding element — **OmniTra*KR***

This makes the intentional spelling memorable and recognisable. Logo, wordmark, and all branding should emphasise the **KR** as a visual feature.

**Domain:** omnitrakr.com

**Tagline ideas:**
- "Track everything you experience"
- "Your all-in-one life tracker"
- "Watch. Read. Play. Listen. Track."

---

## Quick Start

```bash
# Clone and set up
composer create-project laravel/laravel omnitrakr
cd omnitrakr
composer require laravel/breeze --dev
php artisan breeze:install vue --ssr

composer require laravel/socialite laravel/horizon spatie/laravel-query-builder
npm install vue-virtual-scroller @vueuse/core vue-draggable-plus chart.js date-fns

cp .env.example .env
php artisan key:generate

# Start infrastructure via Docker
docker compose up -d postgres redis

# Run migrations and start dev servers
php artisan migrate
php artisan horizon:install
php artisan serve
npm run dev
php artisan horizon
```

For full containerised deployment with all worker containers, see the Docker Compose reference in `ARCHITECTURE.md`.

---