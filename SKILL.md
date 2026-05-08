---
name: bangdream-live-planner
description: Search and compile detailed reports on BanG Dream (Bushiroad) live events, plan travel itineraries around Chinese holidays or user vacation dates, find optimal round-trip flight combinations, and retrieve live-specific details such as venue information and bonus goods images. Use when the user mentions BanG Dream, Bushiroad, live concerts, setlists, tour schedules, fan meeting events, travel planning for lives, flight booking for concerts, or bonus goods (tokuten) inquiries. Outputs comprehensive reports in Markdown or HTML format.
---

# BanG Dream Live Planner

## Overview

This skill helps users discover, research, and plan trips for BanG Dream (and related Bushiroad) live events. It supports three primary modes that can be combined flexibly based on the user's request:

1. **Live Information Research** — Compile comprehensive reports on upcoming or past live events
2. **Travel & Flight Planning** — Match live dates with holidays/vacation and find optimal flights
3. **Live Detail Inquiry** — Deep-dive into specific live events (setlists, venues, bonus goods, images)

## Quick Decision Tree

Determine the user's intent:

- **"What lives are happening?" or "Tell me about upcoming lives"** → Follow [Live Research Mode](#live-research-mode)
- **"I have vacation/holiday on [dates]" or "Plan a trip for me"** → Follow [Travel Planning Mode](#travel-planning-mode)
- **"Tell me about [specific live name]" or "What are the bonus goods?"** → Follow [Live Detail Mode](#live-detail-mode)
- **Combined request** → Execute modes sequentially or in parallel as appropriate

## Live Research Mode

### Step 1: Search for Live Information
Use web search to find official and reliable sources. Key sources include the official BanG Dream website, Bushiroad Music, official Twitter/X accounts, venue websites, and fan wikis.

#### Search Priority Rules

**Rule 1: Exact match first**
If the user explicitly names a specific live, event, album, or tour (e.g., "Roselia 10th live", "Lehre der Rose", "Exitus FINAL"), your **first search must use that exact name or closest variant**. Do not skip over an officially announced event that matches the user's query in favor of inferring a different, future event.

**Rule 2: Favor confirmed, published events**
Always prioritize events that have already been officially announced with concrete dates, venues, and ticket information. Only fall back to inferred or unconfirmed future events if no officially published match exists.

**Rule 3: Keyword expansion**
If the exact search returns limited results, expand with:
- Official Japanese event title + "日程"
- Album name + "リリース記念ライブ"
- Tour name + "ファイナル"
- Band name + "live [year] schedule`
- `[Band name] live tour [year]` (e.g., Poppin'Party, Roselia, RAISE A SUILEN, Morfonica, MyGO!!!!!)

### Step 2: Compile the Report

For each live event, gather:

| Field | Description |
|-------|-------------|
| Event Name | Official Japanese and English names |
| Date(s) | Performance dates and times (JST) |
| Venue | Full venue name, address, capacity |
| Performing Units | Which bands are performing |
| Ticket Info | Price tiers, sale dates, where to buy |
| Setlist | If available (official or fan-reported) |
| Bonus Goods (特典) | Available goods, prices, pre-order info |
| Official Links | Website, streaming info |

### Step 3: Output Format
Generate a comprehensive report in Markdown or HTML. Include a summary table at the top, followed by detailed sections for each event.

## Travel Planning Mode

### Step 0: Visa & Preparation Timeline
Calculate backwards from the departure date and provide a preparation checklist:

- **Japan tourist visa (single entry)**: Apply 1-2 months before travel; processing takes 7-10 business days
- **Japan tourist visa (multiple entry)**: Apply 1-2 months before; processing takes 7-14 business days
- **Passport validity**: Must be valid for 6+ months beyond return date
- **Live ticket purchase**: Fan club pre-sales often open 2-3 months before the event; general sales typically 1 month before
- **Hotel booking**: Book immediately after flights are confirmed (essential during Chinese holidays)
- **Mobile data / pocket WiFi**: Reserve 2 weeks before departure
- **Suica / Pasmo IC card**: Purchase on arrival or set up via mobile app before departure
- **Travel insurance**: Optional but recommended; purchase 1-2 weeks before departure

Output this as a dated checklist so the user knows exactly when each task should be completed.

### Step 1: Identify Available Dates
Ask the user or infer from context:
- Specific vacation dates provided by the user
- Upcoming Chinese public holidays (use web search for current year)
- Weekends adjacent to holidays for extended trips

### Step 2: Match Lives to Dates & Check Ticket Status
Filter the live events that fall within or near the available travel window. Consider:
- Same-day or next-day arrival feasibility
- Multiple lives in one trip (if clustered geographically/temporally)

For each matched live, perform a **ticket status check**:

Search for the latest ticket sale information and classify status:

| Status | Icon | Definition | User Action Required |
|--------|------|------------|-------------------|
| **Available** | 🟢 | Official sales open and tickets still purchasable | Purchase soon |
| **Upcoming Sale** | 🟡 | Sale has not started yet (e.g., fan club pre-sale next week) | Set calendar reminder |
| **Recently Ended** | 🔴 | General sale ended within past 2-4 weeks | Check resale platforms immediately |
| **Long Ended** | ⚫ | Sale ended months ago | Resale platforms only; prices likely inflated |
| **Sold Out** | ⚫ | Officially marked as sold out | Resale platforms only |
| **Unknown** | ⚪ | Cannot determine status from search | Advise user to check official source directly |

**Urgency escalation rules:**
- If any matched live is 🔴 or ⚫ status: output a prominent warning box at the TOP of the report before any other content. State clearly that tickets may be difficult to obtain and list recommended resale platforms.
- If any matched live is 🟡 with sale date within 7 days: output a reminder to set an alarm.
- If all matched lives are 🟢: proceed normally.

Include a **Ticket Status Summary** table in the final report for each event.

### Step 3: Search Flights (MANDATORY ACTUAL SEARCH)

**CRITICAL: You MUST perform actual web searches for real flight prices on the exact travel dates.** Generic price ranges like "¥3,000-4,500" are NOT acceptable. The user needs real, bookable flight data.

#### Mandatory Search Process

1. **Confirm departure city** (ask if unknown; default: Shanghai)
2. **Confirm destination airport**: HND (Haneda) or NRT (Narita) for Tokyo; KIX for Osaka
3. **Search flights using multiple platforms** — you MUST run WebSearch on at least 3 of the following for the exact dates:
   - `携程 flights [出发城市] [目的地] [日期] 往返 价格`
   - `Google Flights [city] to [city] [date] round trip price`
   - `Expedia flights [city] to [city] [date]`
   - `去哪儿网 [出发城市] 飞 [目的地] [日期]`
   - `Skyscanner [city] to [city] [date]`
   - `Ctrip international flights [city pair] [date]`

4. **Search for each candidate date combination** (at least 2-3 date options if flexible):
   - Search query must include specific dates (e.g., "上海飞东京 8月28日 往返 8月30日 2026 机票价格")
   - Also search airline official sites (JAL, ANA, 东航, 国航, 春秋) for direct booking prices

5. **Extract SPECIFIC flight data** — each option MUST include:
   - Airline name and flight number (e.g., MU523, NH920)
   - Departure airport + exact departure time
   - Arrival airport + exact arrival time
   - Total flight duration (direct vs 1-stop)
   - **Exact price** (with currency) — NOT a range
   - Whether checked baggage is included
   - Whether it's a direct flight or requires transfer

6. **Provide at least 3 distinct options** ranked by:
   - **Best Value (推荐)**: Best balance of price + timing + airline quality
   - **Lowest Price**: Cheapest option regardless of inconvenience
   - **Best Comfort**: Best timing (daytime arrival, direct flight, good airline) regardless of price

7. **If flight search yields no specific prices from search results**:
   - Try different search queries and platforms
   - Search the airline's official website directly
   - If still unavailable after multiple attempts, clearly state which platforms were searched, what was found, and tell the user where they can find the actual prices (with direct links)

8. **Far-future flights constraint (3+ months ahead)**:
   - Many airlines only release fares 3-6 months before departure. For flights more than 3 months out, exact prices may not be available via search engines.
   - In this case: search multiple platforms first, then provide the LATEST available prices you CAN find (e.g., 1-2 months ahead data), clearly标注 the date of the data and the flight number/route it applies to.
   - Also provide: (a) known flight schedules (airline, flight number, departure/arrival times), (b) lowest prices found from ANY available date as a reference baseline, (c) DIRECT BOOKING LINKS for the user to check real-time prices for their specific dates.
   - NEVER use prices from a completely different route or season as a proxy without clearly explaining the limitation.

#### Evaluation Criteria

For each flight option, evaluate:
- **Price**: Exact fare (not a range)
- **Total travel time**: Including layovers
- **Departure/arrival times**: Flag red-eye flights (departure 22:00-06:00 or arrival before 06:00)
- **Direct vs transfer**: Direct flights preferred; if 1-stop, include layover duration and transfer airport
- **Baggage**: Whether the fare includes checked luggage
- **Airline quality**: Full-service (JAL/ANA/东航) vs budget (春秋)

**STRICT RULE**: Never output a flight recommendation without having searched for and retrieved actual price data. If you cannot find real prices, explicitly list which platforms you searched and provide direct booking links.

### Step 4: Airport Departure Logistics
For the recommended flight option, provide specific departure logistics:

- **Leave for airport**: International flights require check-in 3 hours before departure; add traffic/metro time from user's location
- **Airport arrival**: Check-in closes 1 hour before departure for most international flights
- **Security & immigration buffer**: 45-60 minutes at major Chinese airports
- **Arrival at destination**: Estimated time to clear immigration and customs
- **Airport to hotel**: Transport route, duration, and cost (Narita Express, Keisei Skyliner, airport bus, limousine bus, etc.)

### Step 5: Build Detailed Daily Itinerary
Create a granular day-by-day schedule with specific times and actionable items.

**Arrival Day:**
- Flight arrival time (local JST)
- Airport to hotel transport (route, duration, approximate cost)
- Hotel check-in time (typically 15:00 in Japan; early check-in may be possible)
- Evening: light exploration or rest recommendation based on arrival time

**Pre-Live / Free Day:**
- Morning: breakfast options near hotel
- If user provides hotel name/area: suggest nearby attractions, walking routes, estimated duration
- Lunch: nearby restaurant recommendations with reservation/queue instructions
- Afternoon options:
  - Anime/otaku shopping (Animate, Gamers, Gee! Store, etc.)
  - Local sightseeing
  - Venue early arrival for goods purchase (typically opens 3-4 hours before doors)

**Live Day:**
- Morning: hotel breakfast or nearby cafe
- Late morning / early afternoon: nearby exploration if time permits
- Travel to venue: departure time from hotel, route, duration
- Venue arrival: recommended time (goods purchase, photo spots, meetups)
- Doors open / live start / estimated end time
- Post-live: return transport to hotel

**Departure Day:**
- Hotel checkout (typically 10:00-11:00)
- Morning activity if flight permits (luggage storage at station or airport)
- Transport to airport: route, duration, recommended departure time from hotel
- Arrive at airport 2-3 hours before international departure

**CRITICAL: Multiple leave-day options**
When the user mentions "请一天假" or similar flexible-date requests, and multiple valid leave-day combinations exist (e.g., 请周五 vs 请周一), you MUST provide **FULL detailed day-by-day itineraries for EVERY option**, NOT just one. Each option's itinerary must include:
- Complete hour-by-hour schedule for each day
- Specific flight times (based on the chosen dates)
- Specific restaurant/attraction recommendations
- Transport routes and times
- Live arrival/departure logistics
Do NOT provide a "简表" or summary for alternative options — they deserve the same level of detail as the primary recommendation.

### Step 6: Hotel & Local Exploration (Optional)
If the user provides hotel information (name, area, or address):

#### Attraction Priority Ranking
When selecting attractions to recommend, apply this priority order:

1. **P0 — Must-See Classics**: Iconic Tokyo/Japan landmarks that are genuinely worth visiting (e.g., Senso-ji, Meiji Shrine, Shibuya Crossing, teamLab, Tokyo Tower, Skytree)
2. **P1 — Anime Pilgrimage (圣地巡礼)**: Real-world locations featured in BanG Dream, Girls Band Cry, or related girl-band anime. These take precedence over generic sightseeing for fans. Use **https://www.anitabi.cn/** and web search to identify specific spots.
3. **P2 — Meme / Internet Culture Landmarks**: Iconic internet-culture locations (e.g., the "Shimokitazawa Beast House" / 下北沢の野獣の家, famous 2chan/5ch meme spots, iconic konbini from viral videos). Include only if reasonably accessible and the user shows interest in meme culture.

**Decision rule**: Always include at least one P0 classic. If P1 pilgrimage spots exist within reasonable travel time (under 45 min from hotel/venue), prioritize them over additional P0 spots. P2 spots are optional seasoning.

#### Information to Provide
- **Nearby attractions**: Within walking distance or 15-20 min by train, tagged by priority (P0/P1/P2)
- **Anime/otaku spots**: Animate, Gamers, Lashinbang, Surugaya, Tower Records, etc.
- **Dining recommendations**: Breakfast, lunch, dinner options with cuisine type, price range, and how to book (Tabelog, phone, walk-in)
- **Reservation/queue notes**: Popular places may require Tabelog reservations or have long queues; note peak times
- **Walking directions or train routes**: Include approximate travel times
- **Convenience stores**: Nearby Lawson, 7-Eleven, FamilyMart for late-night snacks or ATM withdrawals

## Live Detail Mode

### Step 1: Identify the Specific Live
Clarify which live event the user is asking about. Common identifiers:
- Official event name
- Band name + date/venue
- Tour name

### Step 2: Retrieve Detailed Information
Search for:
- Official announcements (setlists, special guests)
- Venue details (seating map, access info)
- Bonus goods (特典): descriptions, images, prices
- Streaming or Blu-ray release info

### Step 3: Retrieve Images
If the user asks about bonus goods visuals or official promotional images:
- Search official websites and Twitter/X posts for image URLs
- Use image generation only if official images are unavailable and user explicitly asks for mockups

### Step 4: Output
Compile into Markdown or HTML with embedded image links.

## Output Guidelines

### Format Selection
Choose the output format dynamically based on content characteristics:

| Format | When to Use | File Extension |
|--------|-------------|----------------|
| **Markdown** | Default. Use for text-heavy reports, itineraries, and live research. Best for readability and copy-paste. | `.md` |
| **HTML** | Use when the output contains many images (e.g., bonus goods visuals), needs rich visual styling, or the user explicitly requests a "web page" style output. | `.html` |
| **Other** | If the user requests a specific format (e.g., PDF, Word doc), use the appropriate skill (pdf, docx) to generate it. | Per skill |

**Decision heuristic:**
- If the report includes 3+ embedded images or image links → prefer **HTML**
- If the user says "做成网页" / "做成可以看的页面" / "HTML" → use **HTML**
- Otherwise → use **Markdown**

### File Naming Convention
When saving output to a file, generate the filename dynamically based on content. Do NOT use fixed generic names.

**Pattern:**
```
[band_or_event]_[date_or_period]_[report_type].[ext]
```

**Examples:**
- `avemujica_exitus_final_2026_june.md`
- `bangdream_dragonboat_holiday_plan.md`
- `roselia_bonus_goods_visuals.html`
- `mygo_9th_live_setlist_report.md`
- `bangdream_2026_h1_live_schedule.md`

Include the band name, event type, date/period, and report type. Keep it concise but descriptive.

### Tone
- Enthusiastic but informative
- Clearly distinguish confirmed information from unofficial/fan-reported data
- Note when information is pending or unconfirmed

### Cost and Currency Rules

All prices in the output MUST clearly distinguish between currencies. NEVER mix currencies or add them together.

| Currency | Format | Use For |
|----------|--------|---------|
| Chinese Yuan (RMB) | `RMB X,XXX` | Flights from China, visa fees, China domestic transport |
| Japanese Yen (JPY) | `JPY X,XXX` | Live tickets, hotels in Japan, ground transport in Japan, meals in Japan, shopping |

**Mandatory rules:**
- **NEVER use the `¥` symbol alone** — it is ambiguous (used for both RMB and JPY). Always use `RMB` or `JPY` prefix.
- **NEVER add amounts in different currencies together** — RMB and JPY have different exchange rates. Do NOT produce a "total cost" that mixes them.
- If the user asks for a rough total: first search the current RMB/JPY exchange rate (e.g., WebSearch "当前人民币日元汇率 2026"), then convert all JPY amounts to RMB (or vice versa), clearly label the exchange rate used and the conversion date, and mark the result as "估算（基于X月X日汇率）".
- If no exchange rate search is needed (user just wants itemized costs): simply list each item with its correct currency prefix. DO NOT produce a combined total.

### Itemized Cost Rules
All cost estimates in the output MUST be based on actual searched data, not generic ranges:
- **Flights**: Use exact prices from search results in RMB (e.g., "RMB 2,380 MU523 08:00-12:30 direct"), NEVER use vague ranges like "RMB 3,000-4,500"
- **Hotels**: Use JPY for Japan hotels; search for actual prices if dates are near, or provide typical price ranges with currency clearly marked as JPY
- **Live tickets**: Use official published prices in JPY
- **Ground transport**: Use known fare data in JPY (train/bus fares are stable)
- **Meals**: Reasonable estimates in JPY are acceptable (restaurant prices are relatively stable)
- If exact prices cannot be found after multiple search attempts, clearly state "未能找到具体价格" and provide a direct link to the booking platform

## Additional Resources
- For detailed search strategies and source reliability, see [reference.md](reference.md)
- For example outputs, see [examples.md](examples.md)
