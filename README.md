# Middle East War — Frontlines

A playable browser strategy vertical slice on real regional geography. Pause, review the theater, issue orders, then watch movement, combat, capture and logistics unfold. **Every deployment, command, capability, resource value and campaign event is fictional.** This is not a current-conflict map.

## Run locally

Use Node **24 LTS**. The data importers use its native TypeScript support. Implemented and checked on **Node v24.18.0 / npm 11.16.0 / Windows x64**. The lockfile pins installed dependency versions.

```powershell
npm ci
npm run data:prepare
npm run data:roads
npm run data:world
npm run data:validate
npm run data:world:validate
npm run dev -- --host 127.0.0.1
```

Open **http://127.0.0.1:5173/**. The scenario starts paused. No backend, commercial map token, remote tile service, or account is required. The prepared pack is already in `public/data`, so `data:prepare` is only needed to verify/rebuild it or acquire a local raw cache on another machine. On a fresh raw-cache acquisition, allow access to the pinned Natural Earth URLs printed by the importer. No substitute country outlines are generated if acquisition fails.

Run data preparation **before** the dev server. On Windows, Vite can lock changed JSON files; stop it and rerun preparation if the importer reports `EPERM`. Cached inputs are checksum-validated and unchanged outputs are not rewritten. `npm run data:prepare -- --update` explicitly re-fetches the same frozen source version for verification.

To try a phone on the same network:

```powershell
npm run dev -- --host 0.0.0.0
```

Open the computer's LAN address on port 5173 and permit it through the local firewall. Actual phone hardware/LAN access has not been certified. Browser storage belongs to each origin; changing host or port uses a separate save slot.

## Play

**القيادة الدولية:** افتح **اختيار دولتي والمضائق** أو اختر دولة من **Countries** ثم **اختيارها لتكون دولتي**. يمكنك إدارة فتح/إغلاق ستة مضائق، مشاهدة طوابير السفن وإعطاء قرارات العبور، وإطلاق مهمات على أي نقطة بالخريطة. توجد طبقة مرجعية لقواعد أميركية معلنة مع مصادرها. أكّد الأوامر ثم استأنف الساعة. التفاصيل العربية في [دليل القيادة الدولية](docs/national-campaign.md).

**القوات والمعارك والدبلوماسية:** لكل دولة جنود وحاميات قابلة للقتال. افتح **القوات والمعارك** لإدارة 1,132 موقعاً، بينها قواعد أميركية بنسخ محصنة داخل اللعبة مع دفاع جوي ومقاتلات ورد آلي. نافذة الاستهداف تسمح بأسراب حتى 16 مسيّرة أو صاروخاً أو طائرة. أرسل قوة برية لاحتلال موقع، أو افتح **الدبلوماسية** لزيارة دولة والتفاوض على وقف نار أو تحالف. المواقع تقريبية والقدرات والأعداد والنتائج افتراضية. تحقق من بيانات الحاميات المشتقة باستخدام `npm run data:campaign:validate`.

1. Select a formation from the map or **Formations**.
2. Choose **Move**, tap a valid land cell or use **Destination list**, then **Confirm**.
3. **Resume** or press Space. Use 1×, 2× or 4×; pause at any time to queue orders.
4. Hold six objectives to gain points every six game hours. Reach 100 points or lead after 30 days. Keep your command center: losing it for 24 hours ends your command.
5. Keep supply connected, recruit in **Logistics**, and negotiate a ceasefire in **Diplomacy**.
6. **Archive** provides save/load, JSON export/import and a new operation as Cedar, Inland or Coast.

For rocket support, select a stationary formation → **Rocket strike** → tap a visible target or choose it from the list → **Launch** → **Resume**. A smoky directional rocket follows the aiming arc and explodes on impact. Each strike costs 40 materiel and 15 fuel; support recharges for 90 game minutes. Pause freezes flight, smoke and explosions.

**Air & rocket support** also offers a Shahed-style delta-wing attack drone, a surveillance drone that reveals its destination area, and a jet airstrike. The house-shaped **Miniature detail** button zooms in on tiny tanks/cars, soldier dots, traffic and isometric houses. Strikes turn houses into persistent rubble and lower stability. See [miniatures and air support](docs/miniatures.md).

Use **World** for the full reference map, **Countries** to search English/Arabic profiles and browse cities, industry, army outposts and ports, and **3D** for a tilted camera with native raised buildings. Industrial districts include warehouses, chimneys, container yards and local streets. Commercial ships follow illustrative shipping lanes and freeze with the simulation. **Region** returns to commandable gameplay. The atlas includes 242 countries/territories, 7,341 cities and 1,081 sourced ports; world industry, outposts and shipping are fictional scenery. See [world atlas](docs/world-atlas.md).

Mobile uses bottom navigation and expandable panels. Move orders support touch without hover/right-click. Keyboard users can select formations and destinations from lists. Space toggles pause, M plans a move, Escape cancels planning or closes a dialog. Reduced motion is respected. Switching away pauses the simulation; returning requires explicit resume, with no offline progression.

## Implemented

- React + strict TypeScript + Vite, direct MapLibre adapter, Zustand, Zod, idb, Vitest and Playwright.
- A frozen local Natural Earth pack with 21 sourced settlement points, contextual Palestinian territories, claim/dispute overlays, attribution and source/status notes.
- A separate 12 km projected land graph; three fictional commands, 24 initial formations, infantry/armor/recon, six objectives.
- Deterministic Web Worker simulation, fixed ticks, tactical pause, speeds and ordered/deduplicated commands.
- A* movement and edge progress, opposite-direction encounters, simultaneous abstract combat, retreats, uncontested capture and objective/defeat conditions.
- Rocket support with visible-target validation, saved projectiles, curved smoke trails, directional flight and expanding impact explosions; reduced-motion rendering is supported.
- Zoom-scaled tanks, cars, soldier dots, isometric city blocks, traffic, saved building damage, reconnaissance/attack drones and jet support. Generalized real road curves use a separately checksummed Natural Earth display pack.
- Graph fog of war, explored-cell memory, timestamped contacts, filtered renderer snapshots and an observation-only utility AI.
- Connected supply, carried reserves, integer resources/upkeep, time-based recruitment/reservations/refunds and production loss on capture.
- Ceasefire proposals, AI responses, effective/expiry ticks, hostile-order cancellation and disengagement without transit rights.
- Atomic IndexedDB current/previous save slots, autosave every four game hours, validated imports and complete-world deterministic persistence.
- Desktop and mobile layouts, list-based map actions, a field log/command queue, explicit missing-data/WebGL states and a development planner preview.

## Check

```powershell
npm run typecheck
npm run test
npm run build
npx playwright install chromium
npm run test:e2e
npm run test:stress
```

Playwright installs Chromium once. The suite starts a local Vite server if needed, or reuses port 5173. On Windows, start `npm run dev -- --host 127.0.0.1` in a separate terminal before testing to reuse that server and avoid child-process teardown delays. `npm run preview -- --host 127.0.0.1` serves the production build on Vite's printed port.

The stress command runs a seeded 100-formation simulation against the real graph and writes environment details, timings and a final world hash to `artifacts/stress-result.json`. It measures simulation computation, **not browser FPS or physical-mobile performance**. `npx tsx scripts/visual-qa.ts` captures desktop/mobile previews from an already-running port 5173 into `artifacts/`.

## Data and limitations

Natural Earth **5.1.2**, public domain, frozen commit **f1890d9f152c896d250a77557a5751a93d494776**. Countries/lakes/rivers are 1:50 million; populated places/disputed areas are 1:10 million. Full URLs, acquisition dates, raw/derived checksums, transformations and content identity are in `public/data/manifest.json`; notices are in `public/data/LICENSE.txt`.

Reference geography, disputes/claims and fictional cell control are independent. The Blue Line is a withdrawal line and is explained separately; reusable verified geometry was not acquired and no precise line is invented. Golan Heights, West Bank, Gaza, Jerusalem and unavailable Shebaa Farms detail have explicit status notes. Natural Earth's default de facto perspective is generalized and has an unknown political effective date; labels need specialist review.

Real elevation, road/bridge topology, construction, trade/transit, advanced diplomacy, full localization, campaign progression, multiplayer and native/store packaging are deferred. Elevation is null and flat/uniform movement terrain is explicitly an abstraction. No real-device performance target or broad geographic/accessibility certification is claimed. This task does not commit, publish or deploy the project.

## Project guide

```text
src/app                 Worker bridge and UI store
src/ui                  Panels, formation inspector and dialogs
src/map                 MapLibre adapter and local label sprites
src/sim                 Deterministic engine and scenario creation
src/sim/pathfinding     Metric-grid A*
src/sim/systems         Visibility and faction observations
src/sim/ai              Observation-only planner
src/worker              Fixed-step scheduler and worker entry point
src/schemas             Commands, saves, geography and scenario schemas
src/persistence         IndexedDB transactions and save envelopes
src/content             Fictional scenario, balance and English keys
scripts/data            Frozen download, processing and validation
public/data             Local browser pack, manifest and license
tests                   Unit, integration and desktop/touch flows
docs                    Architecture, geography, rules and limitations
```

Read [architecture](docs/architecture.md), [geography](docs/geography.md), [game rules](docs/game-rules.md), and [limitations/recovery](docs/limitations.md) for the exact contracts and remaining milestones.
