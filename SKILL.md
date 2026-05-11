---
name: bangdream-live-planner
description: Search and compile detailed reports on BanG Dream (Bushiroad) live events, plan travel itineraries around Chinese holidays or user vacation dates, find optimal round-trip flight combinations, and retrieve live-specific details such as venue information and bonus goods images. Use when the user mentions BanG Dream, Bushiroad, live concerts, setlists, tour schedules, fan meeting events, travel planning for lives, flight booking for concerts, or bonus goods (tokuten) inquiries. Outputs comprehensive reports in Markdown or HTML format.
---

# BanG Dream Live Planner

## Overview

This skill helps users discover, research, and plan trips for BanG Dream (and related Bushiroad) live events. It supports four primary modes that can be combined flexibly based on the user's request:

1. **Live Information Research** — Compile comprehensive reports on upcoming or past live events
2. **Travel & Flight Planning** — Match live dates with holidays/vacation and find optimal flights
3. **Live Detail Inquiry** — Deep-dive into specific live events (setlists, venues, bonus goods, images)
4. **Location-First Discovery** — User names a destination city and time window; search for live events in/near that city and build a trip around them

## Quick Decision Tree

Determine the user's intent **in this exact priority order**:

1. **Does the user explicitly name a Japanese city/region AND a time window?** (e.g., "我想去福冈", "大阪有什么Live", "札幌那几天", "东京端午节") → Follow [Location-First Mode](#location-first-mode) — this takes precedence when both location and dates are present.

2. **Does the user name a specific live/event/band?** (e.g., "Roselia 10th live", "Ave Mujica FINAL", "MyGO!!!!! 特典") → Follow [Live Detail Mode](#live-detail-mode) if asking for details, or [Travel Planning Mode](#travel-planning-mode) if asking to plan a trip around it.

3. **Does the user mention vacation/holiday/dates without specifying a location?** (e.g., "端午节有三天假", "请一天假去看Live", "帮我安排行程") → Follow [Travel Planning Mode](#travel-planning-mode).

4. **Is the user asking about upcoming lives generally, without a location or specific event?** (e.g., "最近有什么Live", "接下来有什么演出") → Follow [Live Research Mode](#live-research-mode).

5. **Combined or ambiguous request** → Execute modes sequentially or in parallel as appropriate, then let the user choose.

**Key rule**: Location-First Mode is ONLY triggered when the user explicitly mentions a Japanese city/region. If no city is mentioned, fall back to the original Live Research / Travel Planning / Live Detail logic as before.

## Live Research Mode

### Step 1: Search for Live Information
**CRITICAL: All live event information MUST be sourced from official Bushiroad / BanG Dream channels ONLY.**

Acceptable official sources (in priority order):
1. **bang-dream.com** (official website — highest priority)
2. **bushiroad.com / bushiroad-music.com** (official corporate/music site)
3. **Official Twitter/X accounts**: @bang_dream_info, @bang_dream_mygo, band-specific accounts
4. **Official PR releases** (e.g., PR TIMES with Bushiroad as publisher)
5. **Venue websites** (when linked from official channels)

**UNACCEPTABLE sources for factual claims** (may be used ONLY for supplementary context, and MUST be labeled as such):
- Fan wikis (萌娘百科, Bandori Wiki, Fandom, etc.)
- Social media reposts / unofficial translations
- Third-party ticketing or event aggregator sites
- Rumor / speculation posts

**If official information is unavailable or incomplete, you MUST state this explicitly.** Do not fill in gaps with inference, assumption, or unofficial sources. Use clear labels like:
- "官方尚未公布" (officially not yet announced)
- "信息来源：非官方渠道，仅供参考" (non-official source, for reference only)
- "待确认" (pending confirmation)

#### Search Priority Rules

**Rule 1: Exact match first**
If the user explicitly names a specific live, event, album, or tour (e.g., "Roselia 10th live", "Lehre der Rose", "Exitus FINAL"), your **first search must use that exact name or closest variant** on official channels (bang-dream.com, official PR). Do not skip over an officially announced event that matches the user's query in favor of inferring a different, future event.

**Rule 2: Official source validation + verbatim citation**
Before including any fact (date, venue, price, lineup, setlist, ticket status, ticket rules) in the output, verify that it appears on an official source. If you cannot verify via an official source, mark it explicitly. **Never present unverified information as confirmed fact.**

**CRITICAL: For ticket rules, pricing tiers, and application conditions, you MUST capture the official Japanese/Chinese verbatim text (or a faithful translation) and cite it in the output.** Do NOT paraphrase or summarize from memory. If the rule is complex (e.g., "how many days one serial can apply for"), quote the official wording directly or attach a clear translation with the source URL. This prevents misrepresentation of multi-day application rules, ticket limits, and eligibility conditions.

**Rule 3: Favor confirmed, published events**
Always prioritize events that have already been officially announced with concrete dates, venues, and ticket information on bang-dream.com or Bushiroad PR. Only fall back to inferred or unconfirmed future events if no officially published match exists, and label them clearly.

**Rule 4: Keyword expansion**
If the exact search returns limited results, expand with:
- Official Japanese event title + "日程 site:bang-dream.com"
- Album name + "リリース記念ライブ site:bang-dream.com"
- Tour name + "ファイナル site:bang-dream.com"
- `[Band name] live [year] site:bang-dream.com` (e.g., Poppin'Party, Roselia, RAISE A SUILEN, Morfonica, MyGO!!!!!)

### Step 2: Compile the Report

For each live event, gather **ONLY from official sources** (bang-dream.com, bushiroad.com, official PR, official social media):

| Field | Description | Source Requirement |
|-------|-------------|-------------------|
| Event Name | Official Japanese and English names | Official site / PR |
| Date(s) | Performance dates and times (JST) | Official site / PR |
| Venue | Full venue name, address, capacity | Official site / venue site |
| Performing Units | Which bands are performing | **MANDATORY: Only list if officially announced** |
| Ticket Info | Price tiers, sale dates, where to buy | Official site / eplus / official ticket page |
| Ticket Rules | Application limits, serial usage rules, multi-day eligibility | **MANDATORY: Quote official verbatim text** |
| Setlist | If available | Official Blu-ray/streaming only; fan-reported must be labeled |
| Bonus Goods (特典) | Available goods, prices, pre-order info | Official site / PR |
| Official Links | Website, streaming info | Direct link to bang-dream.com or official source |

**In the final output, you MUST add a source note for every event**, listing which official source(s) the information came from. If any field could not be verified from an official source, explicitly state "官方尚未公布" for that field.

### Step 3: Output Format
Generate a comprehensive report in Markdown or HTML. Include a summary table at the top, followed by detailed sections for each event.

## Location-First Mode

Use this mode when the user names a Japanese city/region and a time window (holiday, vacation, or date range) and asks what live events are happening there. The priority is: **place first, then find lives**.

### Step 1: Identify the Destination & Time Window

Extract from the user's message:
- **Target city/region** (e.g., 福冈, 大阪, 东京, 札幌, 名古屋, 横滨, 广岛, 仙台)
- **Date range** — specific dates, a holiday name (e.g., 春节, 五一, 国庆), or a relative window (e.g., "下个月", "端午节前后")

If the date range is a Chinese holiday, perform the same mandatory holiday verification as in [Travel Planning Mode Step 1](#step-1-identify-available-dates).

### Step 2: Map the City to Key Venues

Consult [reference.md](reference.md) for the venue index of the target city. Major cities and their typical BanG Dream live venues:

| City | Major Venues | Airport |
|------|-------------|---------|
| **Tokyo** | Zepp DiverCity, Zepp Haneda, Tokyo Garden Theater, Yokohama Arena, Nippon Budokan, Saitama Super Arena, LINE CUBE SHIBUYA, EX THEATER ROPPONGI, TACHIKAWA STAGE GARDEN | HND / NRT |
| **Osaka** | Zepp Namba, Zepp Osaka Bayside, Osaka-Jo Hall, Intex Osaka, Osaka Castle Music Hall, Orix Theater | KIX |
| **Nagoya** | Zepp Nagoya, Nippon Gaishi Hall, Aichi Sky Expo | NGO |
| **Fukuoka** | Zepp Fukuoka, Marine Messe Fukuoka, Fukuoka Sunpalace, Fukuoka Convention Center | FUK |
| **Sapporo** | Zepp Sapporo, Makomanai Sekisuiheim Ice Arena, Hokkaido Prefectural Sports Center, Sapporo Cultural Arts Theater | CTS / OKD |
| **Yokohama** | Yokohama Arena, Pacifico Yokohama, KT Zepp Yokohama | HND |
| **Hiroshima** | Zepp DiverCity Hiroshima, Hiroshima Green Arena, Hiroshima Bunka Gakuen HBG Hall | HIJ |
| **Sendai** | Zepp Sendai, Sendai Sunplaza Hall, Xebio Arena Sendai | SDJ |

### Step 3: Search for Lives in the City/Region

**Search strategy** (execute in this order):

1. **Official site search first**: `site:bang-dream.com [city name] ライブ [year]` (e.g., `site:bang-dream.com 福岡 ライブ 2026`)
2. **Venue-specific search**: `[venue name] バンドリ` or `[venue name] BanG Dream`
3. **General web search**: `BanG Dream live [city] [year]`, `バンドリ ライブ [city] [year]`, `[band name] live [city] [date range]`
4. **Tour/festival search**: Check if any announced tour includes the city as a stop (e.g., Roselia tour stops, Ave Mujica tour schedule)

**For each live found, collect:**
- Event name, date(s), venue (exact name)
- Performing bands
- Ticket status (same classification as Travel Planning Mode)
- Distance/travel time from the target city center (if venue is in a neighboring city)

### Step 4: Present Findings & Recommendations

Structure the output as a **city-first discovery report**:

1. **City Overview** — Brief intro to the city and its anime/music scene relevance
2. **Live Events Found** — Table of all BanG Dream / Bushiroad lives in the region during the window
3. **Recommendation Ranking** — Rank events by:
   - **Match quality**: How well the date fits the user's window
   - **Band popularity / significance**: Major anniversary lives, final tours, etc.
   - **Ticket availability**: 🟢 > 🟡 > 🔴 > ⚫
   - **Venue accessibility**: Proximity to city center, transport convenience
4. **Travel Logistics Preview** — Brief note on flights to that city and typical hotel areas
5. **Next Steps** — Offer to proceed to full [Travel Planning Mode](#travel-planning-mode) for any chosen event

**If NO lives are found**, be honest and suggest:
- Nearby cities with lives in the same window (e.g., "福冈没有找到，但同期大阪有一场...")
- Alternative dates when lives are known to happen in that city
- General sightseeing recommendations for the city as a fallback

---

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

**MANDATORY: You MUST perform actual web searches for Chinese public holiday arrangements, including workday adjustments (调休).** Do NOT assume holiday dates or assume "no workday adjustments."

Search requirements:
- Search for "国务院办公厅关于[年份]年部分节假日安排的通知" or equivalent authoritative source
- Extract the **exact holiday dates**, **workday adjustments (调休)**, and **which weekend days are swapped to workdays**
- Verify from at least one authoritative source (国务院/政府官网, 人民网, 新华社, 或百度百科引用官方通知)

For each holiday, record:
- Official holiday period (start and end dates)
- Number of days off
- Which dates are moved from weekends to workdays (调休上班日)
- Whether adjacent weekends create a natural long weekend

Then identify available travel windows:
- Specific vacation dates provided by the user
- Upcoming Chinese public holidays (with verified调休)
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

**NEVER assume the user does or does not have a specific day off.** Do not write "周五请假" or "周一不用请假" as a default. Instead, present multiple options that cover different leave-day combinations and let the user choose.

**For each option, clearly label:**
- Which date(s) the user would need to take leave
- Which dates fall on weekends or public holidays
- Whether red-eye/late-night flights are involved and what that implies for work schedule

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
When the user mentions "请一天假" or similar flexible-date requests, or when the live falls on a weekend requiring potential leave days, you MUST provide **FULL detailed day-by-day itineraries for EVERY valid leave-day combination**, NOT just one. For example, if a live is on Saturday-Sunday, present itineraries for:
- Option A: Take leave on Friday (early departure)
- Option B: Take leave on Monday (late return)
- Option C: Red-eye flight Friday after work, no Friday leave needed
- Option D: Red-eye flight Sunday after live, no Monday leave needed
- And any other plausible combination

Each option's itinerary must include:
- Complete hour-by-hour schedule for each day
- Specific flight times (based on the chosen dates)
- Specific restaurant/attraction recommendations
- Transport routes and times
- Live arrival/departure logistics
- A clear statement of which day(s) require leave

Do NOT provide a "简表" or summary for alternative options — they deserve the same level of detail as the primary recommendation. Do NOT recommend a single "best" option as if it is the only reasonable choice.

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
| **PDF** | **DEFAULT.** All live planning reports must be output as PDF unless the user explicitly requests otherwise. PDF is the optimal format for mobile viewing, sharing, and preserving exact formatting (tables, fonts, spacing). | `.pdf` |
| **HTML** | Use when the user explicitly requests a web page, or when PDF generation fails and HTML is provided as a fallback with browser print-to-PDF instructions. | `.html` |
| **Markdown** | Use ONLY when the user explicitly requests Markdown (e.g., "给我md文件" / "我要markdown" / "给我文本版"). Never default to Markdown. | `.md` |
| **Other** | If the user requests a specific format not listed above (e.g., Word doc, PPT), use the appropriate skill (pdf, docx, pptx) to generate it. | Per skill |

### PDF Generation (Default Output)

**Every report from this skill MUST attempt to produce a PDF as the final deliverable.** The workflow is:

1. **Generate a high-quality HTML file** first, with mobile-responsive CSS, clean tables, and proper typography.
2. **Convert the HTML to PDF** using the best available tool in the environment.
3. **If PDF conversion succeeds**, deliver the `.pdf` file to the user.
4. **If PDF conversion fails**, deliver the `.html` file and include a short note explaining how the user can save it as PDF via their browser.

#### HTML → PDF Conversion Methods (try in this order)

**Method 1: Python + WeasyPrint (preferred)**
```python
from weasyprint import HTML, CSS
HTML('report.html').write_pdf('report.pdf', stylesheets=[CSS(string='@page { margin: 1cm }')])
```
- Best CSS support, handles tables and fonts well
- Requires `weasyprint` and GTK dependencies

**Method 2: Python + Playwright**
```python
from playwright.sync_api import sync_playwright
with sync_playwright() as p:
    browser = p.chromium.launch()
    page = browser.new_page()
    page.goto('file:///path/to/report.html')
    page.pdf(path='report.pdf', format='A4', margin={'top': '1cm', 'bottom': '1cm'})
    browser.close()
```
- Requires `playwright` and a Chromium browser binary
- Most reliable for complex layouts

**Method 3: Node.js + Puppeteer**
```javascript
const puppeteer = require('puppeteer');
(async () => {
  const browser = await puppeteer.launch();
  const page = await browser.newPage();
  await page.goto('file:///path/to/report.html', {waitUntil: 'networkidle0'});
  await page.pdf({path: 'report.pdf', format: 'A4', margin: {top: '1cm', bottom: '1cm'}});
  await browser.close();
})();
```
- Requires `node`, `npm`, and `puppeteer`

**Method 4: Headless browser via CLI**
```bash
# Chrome/Chromium/Edge
chromium --headless --disable-gpu --print-to-pdf=output.pdf file:///path/to/report.html

# Edge on Windows
msedge --headless --disable-gpu --print-to-pdf=output.pdf file:///path/to/report.html
```
- Requires a Chromium-based browser installed on the system

**Method 5: wkhtmltopdf**
```bash
wkhtmltopdf --page-size A4 --margin-top 10 --margin-bottom 10 report.html report.pdf
```

**Method 6: pandoc**
```bash
pandoc report.html -o report.pdf --pdf-engine=xelatex -V geometry:margin=1cm
```

#### Environment Detection

At runtime, probe the environment to determine which conversion method is available:
```bash
python -c "import weasyprint" 2>/dev/null && echo "weasyprint"
python -c "import playwright" 2>/dev/null && echo "playwright"
command -v chromium 2>/dev/null && echo "chromium"
command -v wkhtmltopdf 2>/dev/null && echo "wkhtmltopdf"
command -v pandoc 2>/dev/null && echo "pandoc"
```

Use the **first available method** from the list above. Do not attempt to install dependencies unless explicitly instructed by the user.

#### PDF Styling Requirements

- Page size: A4 (portrait)
- Margins: at least 1cm on all sides
- Body font size: minimum 10pt; headings: 14pt+
- Tables: preserve borders, use alternating row backgrounds for readability
- Page breaks: insert before each major section (`page-break-before: always`)
- Header/footer: include report title and generation date
- Color profile: optimize for screen reading (not print-optimized grayscale)

#### Fallback Strategy

If **no conversion tool is available** in the current environment:
1. Output the `.html` file with a `<meta name="viewport">` tag and mobile-responsive CSS
2. Include a visible button or instruction in the HTML: "点击浏览器菜单 → 打印 → 另存为 PDF"
3. In your response to the user, explain: "当前环境缺少 PDF 转换工具，已输出优化排版的 HTML 文件。您可以在手机浏览器中打开后通过「打印→另存为 PDF」一键转换。"
4. Provide platform-specific instructions (iOS Safari share sheet → Print → pinch to preview → Share → Save to Files; Android Chrome → Menu → Share → Print → Save as PDF)

**Decision heuristic:**
- **DEFAULT**: Always attempt PDF output
- If the user explicitly says "给我markdown" / "给我md" / "给我文本版" → use **Markdown**
- If the user explicitly says "做成网页" / "给我HTML" / "要网页版" → use **HTML**
- If PDF generation fails → fallback to **HTML** with print-to-PDF instructions
- Never default to Markdown

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
- **Radically honest about information gaps**: If you cannot find official confirmation for a piece of information, say so plainly. Never invent, infer, or embellish to make the report look more complete.
- **Clearly distinguish confirmed information from unofficial/fan-reported data**: Use inline labels like "【官方确认】" or "【非官方/待确认】" where appropriate.
- **Source transparency**: Every event in the report must be traceable to an official source. Include a "Sources" section at the end of the report listing all official URLs consulted.
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

### Cost Estimate Rules
- **Live tickets**: Always list official published prices in JPY.
- **Flights / Hotels / Ground transport / Meals**: Provide exact prices when available from searches. If exact prices cannot be found, state "未能找到具体价格" and provide a direct link.
- **DO NOT provide a lump-sum "total estimated cost" or "budget summary" table** unless the user explicitly asks for one. Many users find aggregated estimates unhelpful or arbitrary. Instead, list each item with its correct currency prefix and let the user do their own math.
- If the user asks "大概要花多少钱", you may provide a brief verbal estimate in prose, but avoid structured tables that mix currencies into a pseudo-total.

## Additional Resources
- For detailed search strategies and source reliability, see [reference.md](reference.md)
- For example outputs, see [examples.md](examples.md)
