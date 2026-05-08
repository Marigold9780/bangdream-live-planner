# Examples: BanG Dream Live Planner

## Example 1: Live Information Research

**User Input:**
> "我想知道未来BanG Dream有什么Live活动"

**Agent Action:**
1. Search for `BanG Dream live 2026 schedule` and `バンドリ ライブ 2026`
2. Check official sources: bang-dream.com, Bushiroad Music, official Twitter
3. Compile all announced lives into a report

**Output Preview:**
```markdown
# BanG Dream Live Report — Upcoming Events

## Summary
| Date | Event Name | Venue | Performing Units |
|------|-----------|-------|------------------|
| 2026-06-15 | Roselia Live: [Title] | Tokyo Garden Theater | Roselia |
| 2026-07-20 | MyGO!!!!! 4th LIVE | Yokohama Arena | MyGO!!!!! |
| 2026-08-10 | BanG Dream! 10th Anniversary Live | Fuji-Q Highland | Multiple bands |

## Roselia Live: [Title]
### Basic Info
- Date: June 15, 2026 (Mon) — Doors 17:00 / Start 18:00 JST
- Venue: Tokyo Garden Theater (東京ガーデンシアター)
- Address: 1-1-2 Shinkiba, Koto-ku, Tokyo

### Ticket Information
- Price: ¥8,800 (General) / ¥10,800 (Premium Seat)
- Sale Period: Fan club pre-sale Apr 1-7; General sale Apr 20
- Purchase: eplus, Lawson Ticket

### Setlist
*Not yet announced. Will be updated after event.*

### Bonus Goods (特典)
- Event-exclusive acrylic stand: ¥1,500
- Live T-shirt (5 designs): ¥3,500 each
- Towel: ¥2,000

### Official Links
- https://bang-dream.com/event/xxxxx
```

---

## Example 2: Travel Planning with Holiday Matching

**User Input:**
> "我五一劳动节有假期，帮我看看有没有合适的Live可以去看，顺便规划一下行程和机票"

**Agent Action:**
1. Determine 2026 Labor Day holiday dates (May 1-5, 2026)
2. Search for BanG Dream lives scheduled around May 1-5, 2026
3. Find 2-3 viable live events within the window
4. Search round-trip flights from Shanghai (default assumption) to Tokyo
5. Compare flight options by price and comfort
6. Compile travel itinerary

**Output Preview:**
```markdown
# Travel Plan: Labor Day Holiday 2026

## Your Holiday Window
- May 1 (Fri) — May 5 (Tue), 2026

## Matching Live Events
| Live | Date | Venue | Fit |
|------|------|-------|-----|
| Poppin'Party Live Tour Final | May 3 (Sun) | Tokyo Garden Theater | Perfect fit |
| RAISE A SUILEN LIVE 2026 | May 4 (Mon) | Zepp DiverCity | Perfect fit |

## Recommended Itinerary: Poppin'Party May 3

### Live Details
- Date: May 3, 2026 (Sun) — Start 17:00 JST
- Venue: Tokyo Garden Theater

### Flight Options (Shanghai ↔ Tokyo)
| Option | Route | Departure | Return | Price | Notes |
|--------|-------|-----------|--------|-------|-------|
| A | PVG → HND (Direct) | May 2, 09:00 | May 4, 18:00 | ¥3,200 | Best comfort, morning arrival |
| B | PVG → NRT (Direct) | May 2, 22:00 | May 4, 21:00 | ¥2,400 | Red-eye departure, cheaper |
| C | SHA → HND (1-stop) | May 2, 14:00 | May 5, 10:00 | ¥2,100 | Cheapest, but 5h layover |

### Recommended Schedule
- **May 2 (Sat)**: Depart Shanghai morning → Arrive Tokyo afternoon → Check in hotel → Explore area
- **May 3 (Sun)**: Live day! Arrive venue by 15:00 → Live 17:00-20:00 → Buy goods → Return to hotel
- **May 4 (Mon)**: Tokyo sightseeing / shopping for anime goods → Evening flight home

### Estimated Total Cost
- Flight (Option A): ¥3,200
- Live ticket: ~¥8,800
- Hotel (2 nights): ~¥20,000
- **Total**: ~¥32,000 (~¥1,600 RMB)
```

---

## Example 3: Specific Live Detail Inquiry with Images

**User Input:**
> "我想了解一下Roselia下一场Live的特典长什么样子，有图吗？"

**Agent Action:**
1. Identify Roselia's next announced live
2. Search for official bonus goods announcement
3. Retrieve official images from Twitter/X or official website
4. Compile detail report

**Output Preview:**
```markdown
# Roselia Live — Bonus Goods Detail

## Event
Roselia Live: [Title]  
Date: June 15, 2026  
Venue: Tokyo Garden Theater

## Bonus Goods (特典)

### 1. Event-Exclusive Acrylic Stand
- Price: ¥1,500
- Design: Individual member stands (5 types)
- Size: Approx. 15cm
- **Image**: ![Acrylic Stand](https://official-image-url.jpg)

### 2. Live T-Shirt
- Price: ¥3,500
- Color: Black base with rose motif
- Sizes: S/M/L/XL
- **Image**: ![T-Shirt](https://official-image-url.jpg)

### 3. Penlight (Blade)
- Price: ¥3,000
- Color: Rose pink (Roselia official color)
- **Image**: ![Penlight](https://official-image-url.jpg)

### Purchase Notes
- Goods sold at venue on live day
- Some items may have purchase limits
- Early arrival recommended for popular items

## Official Source
- Announcement: https://bang-dream.com/event/xxxxx
- Image source: @bang_dream_info (Twitter/X)
```

---

## Example 4: Combined Request

**User Input:**
> "今年春节我想去日本看Live，你帮我看看BanG Dream有没有合适的场次，还想知道特典有什么，然后给我规划一下机票"

**Agent Action:**
1. Determine 2026 Spring Festival dates (late Jan / early Feb)
2. Search for lives in that window
3. For matching lives, gather: basic info + bonus goods + images
4. Search flights from user's home city to Japan
5. Combine all into one comprehensive Markdown report with multiple sections

**Key Principle:** When requests combine multiple modes, execute them in parallel where possible, then weave results into a single cohesive document.

---

## Example 5: Granular Travel Plan with Hotel & Local Exploration

**User Input:**
> "我订了东京有明地区的酒店，想去看一场在Tokyo Garden Theater的Live。帮我做个详细的行程，包括什么时候该办签证、什么时候去机场，还有酒店附近有什么好玩的和好吃的。"

**Agent Action:**
1. Confirm live date and hotel name/address
2. Build preparation timeline (visa, ticket, hotel, WiFi)
3. Search flights and select optimal option
4. Calculate exact airport departure logistics
5. Research Tokyo Garden Theater area and nearby attractions
6. Find dining options near hotel and venue
7. Build hour-by-hour itinerary for each day

**Output Preview:**
```markdown
# Complete Travel Plan: Roselia Live at Tokyo Garden Theater

## Your Live
- **Event**: Roselia Live: [Title]
- **Date**: June 15, 2026 (Mon)
- **Doors**: 17:00 / **Start**: 18:00 JST
- **Venue**: Tokyo Garden Theater (東京ガーデンシアター)
- **Address**: 1-1-2 Shinkiba, Koto-ku, Tokyo

---

## Preparation Timeline

| Task | Complete By | Notes |
|------|-------------|-------|
| Apply for Japan single-entry visa | April 15, 2026 | Processing 7-10 days; apply via Ctrip or embassy |
| Purchase live ticket | April 20, 2026 | General sale opens; use eplus or Lawson Ticket |
| Book hotel (confirmed) | Already done | [Hotel Name] in Ariake area |
| Reserve pocket WiFi | June 1, 2026 | Pick up at Narita/Haneda airport counter |
| Set up Suica on phone | June 10, 2026 | Add to Apple Wallet / Google Wallet |
| Check passport validity | June 1, 2026 | Must be valid until December 2026 |

---

## Flight & Airport Logistics

### Recommended Flight
- **Outbound**: June 14 (Sun) — China Eastern MU523, PVG → NRT, 09:15 → 13:30 JST
- **Return**: June 16 (Tue) — China Eastern MU524, NRT → PVG, 16:00 → 18:30 CST
- **Price**: ¥3,400 round-trip (includes 23kg checked bag)

### June 14 — Departure Day (Shanghai)
| Time | Action |
|------|--------|
| 05:15 | Leave home for Pudong Airport (taxi/Didi, ~45 min) |
| 06:15 | Arrive at PVG Terminal 1 |
| 06:15–07:15 | Check-in, security, immigration |
| 07:15–09:15 | Duty-free, lounge, or wait at gate |
| 09:15 | Depart Shanghai |

### Arrival in Tokyo
| Time | Action |
|------|--------|
| 13:30 | Land at Narita Terminal 2 |
| 13:30–14:30 | Immigration, baggage claim, customs |
| 14:30–15:30 | Narita Express to Tokyo Station (¥3,070, ~60 min) |
| 15:30–16:15 | JR Keiyo Line to Shin-Kiba, then Yurikamome to Ariake-Tennis-no-mori |
| 16:15 | Arrive at hotel area |
| 16:30 | Check in (or drop luggage if early) |

---

## Hotel & Neighborhood Guide

**Your Hotel Area**: Ariake / 有明 (Koto-ku, Tokyo)

### Nearby Attractions (Walking or Short Train)
| Spot | Distance | Time | What to Do |
|------|----------|------|------------|
| teamLab Planets Tokyo | 10 min walk | 2-3 hours | Immersive digital art museum; book tickets 1-2 weeks ahead |
| Odaiba Seaside Park | 15 min walk | 1 hour | Waterfront views, Statue of Liberty replica, evening lights |
| DiverCity Tokyo Plaza | 20 min walk | 2-3 hours | Shopping, Gundam Unicorn statue (transforms at 11:00/13:00/15:00/17:00) |
| Palette Town / Giant Sky Wheel | 15 min walk | 1 hour | Iconic Odaiba Ferris wheel (great night view) |
| Tokyo Big Sight | 5 min walk | 30 min | Famous convention center; interesting architecture |

### Dining Near Your Hotel

**Breakfast**
- **Hotel breakfast**: Check if your hotel includes breakfast
- **Convenience store**: Lawson Ariake [Address] — 3 min walk; onigiri, sandwiches, coffee (~¥500)
- **Doutor Coffee**: Odaiba area — 15 min walk; toast set (~¥600)

**Lunch**
- **Aqua City Odaiba Food Court**: 20 min walk — multiple options including ramen, curry, sushi (~¥1,000-1,500)
- **Saizeriya Ariake**: 10 min walk — Italian chain, budget-friendly, no reservation needed (~¥800-1,200)
- **Kua'Aina Odaiba**: 20 min walk — Hawaiian burger joint with waterfront view (~¥1,500)

**Dinner**
- **Tsukada Nojo Ariake**: 10 min walk — chicken hot pot (mizutaki), reservation recommended via Tabelog (~¥2,500-3,500)
- **Aloha Table Odaiba**: 20 min walk — Hawaiian casual dining, walk-in usually OK (~¥2,000)
- **Gonpachi Nishi-Azabu** (if venturing to Shibuya area): famous izakaya, reservation via Tabelog or phone (~¥3,000-4,000)

**Reservation Notes**
- For Tsukada Nojo: book 3-5 days ahead on Tabelog or call the restaurant
- Most mall food court places do not take reservations; aim for 11:30 or 14:00 to avoid queues
- If you want premium sushi or teppanyaki near Odaiba, book 1-2 weeks ahead

---

## Day-by-Day Itinerary

### Day 1 — June 14 (Sun): Arrival & Light Exploration
| Time | Activity |
|------|----------|
| 05:15 | Leave for Shanghai Pudong Airport |
| 09:15 | Depart Shanghai |
| 13:30 | Arrive Narita |
| 16:30 | Check in at hotel |
| 17:30–19:00 | Rest / freshen up |
| 19:00–20:30 | Walk to Odaiba Seaside Park for night waterfront views |
| 20:30–21:30 | Dinner at Aqua City Odaiba food court or nearby izakaya |
| 22:00 | Return to hotel; sleep early for live day |

### Day 2 — June 15 (Mon): Live Day!
| Time | Activity |
|------|----------|
| 08:00 | Wake up, hotel breakfast or Lawson run |
| 09:00–11:30 | Morning: teamLab Planets (if pre-booked) OR walk around Tokyo Big Sight |
| 11:30–13:00 | Lunch at Saizeriya Ariake or Aqua City |
| 13:00–14:00 | Return to hotel; change into live attire; rest |
| 14:00–14:30 | Travel to Tokyo Garden Theater (Yurikamome or walk, ~10 min) |
| 14:30–16:30 | **Goods purchase window** — arrive early for popular items |
| 16:30–17:00 | Find seat / standing position, buy drinks, use restroom |
| 17:00 | Doors open |
| 18:00 | Live starts |
| ~20:30 | Live ends (estimated) |
| 20:30–21:30 | Post-live goods (if missed), meet friends, take photos |
| 21:30–22:00 | Walk back to hotel |
| 22:30 | Late dinner: convenience store onigiri / nearby ramen if hungry |

### Day 3 — June 16 (Tue): Departure
| Time | Activity |
|------|----------|
| 08:00 | Wake up, breakfast |
| 09:00–11:00 | Final shopping: DiverCity Tokyo Plaza or hotel area souvenir hunt |
| 11:00 | Hotel checkout; leave luggage at hotel front desk |
| 11:30–12:30 | Lunch near hotel |
| 12:30–13:30 | Yurikamome → JR Keiyo Line → Tokyo Station → Narita Express |
| 13:30 | Arrive at Narita Airport |
| 13:30–14:30 | Check-in, security, immigration, duty-free shopping |
| 16:00 | Depart Tokyo |
| 18:30 | Arrive Shanghai |

---

## Total Estimated Cost
| Item | Amount |
|------|--------|
| Flight (round-trip) | ¥3,400 |
| Live ticket | ¥8,800 |
| Hotel (2 nights) | ~¥25,000 |
| Airport/Local transport | ~¥5,000 |
| Meals (2.5 days) | ~¥10,000 |
| Goods/Shopping | ~¥5,000–15,000 (optional) |
| **Total (excluding shopping)** | ~¥52,200 (~¥2,600 RMB) |
```
