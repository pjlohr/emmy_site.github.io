---
permalink: /concerts/
title: Concerts
layout: splash
author_profile: false
header:
  overlay_color: "#000"
  overlay_filter: "0.35" # 0–1 darkens image
  overlay_image: /assets/sandstone.jpg

feature_row:
  - image_path: /assets/concert_images/violins_of_hope.jpg
    # alt: "Performances"
    title: "Violins of Hope with Jewish Museum Milwaukee"
    excerpt: |
          Works by Bloch, Shostakovich, Schoenfield, and others  
          Stefanie Jacob, piano  
          Scott Tisdel, cello  
          Emmy Tisdel Lohr, violin 
    url: https://jewishmuseummilwaukee.org/event/nashama/
    btn_label: "Tickets / More Info"
    btn_class: "btn--primary"
    badge_date: 2025-11-03   # ← ISO date (auto-formats to NOV / 3)


  - image_path: /assets/concert_images/candlelight.jpg
    # alt: "Media"
    title: "Candlelight Concert"
    excerpt: |
      Rock Classics  
      Santa Fe 
    url: https://feverup.com/m/369543
    btn_label: "Tickets / More Info"
    btn_class: "btn--primary"
    badge_month: OCT          # ← manual
    badge_day: 31

  - image_path: /assets/concert_images/candlelight.jpg
    # alt: "Studio"
    title: "Candlelight Concert"
    excerpt: |
      Coldplay x Imagine Dragons  
      Santa Fe 
    url: https://feverup.com/m/369545
    btn_label: "Tickets / More Info"
    btn_class: "btn--primary"
    badge_date: 2025-12-12
---

<style>
/* Calendar badge that overlays the teaser image in each feature tile */
.feature__item .archive__item-teaser {
  position: relative; /* anchor for absolute badge */
}

.mm-calendar-badge {
  position: absolute;
  top: 10px;
  right: 10px;
  width: 58px;
  height: 64px;
  border-radius: 10px;
  overflow: hidden;
  display: inline-flex;
  flex-direction: column;
  align-items: center;
  justify-content: stretch;
  box-shadow: 0 2px 6px rgba(0,0,0,.28);
  z-index: 3;
}

/* Red header with month */
.mm-cal-header {
  background: #e63946;     /* adjust to your brand */
  color: #fff;
  font-weight: 700;
  font-size: 12px;
  letter-spacing: .5px;
  text-transform: uppercase;
  line-height: 1;
  padding: 6px 0 6px;
  text-align: center;
}

/* White body with day number */
.mm-cal-day {
  background: #fff;
  color: #111;
  font-weight: 800;
  font-size: 22px;
  line-height: 1;
  flex: 1 1 auto;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Optional: subtle border for dark images */
.mm-calendar-badge {
  border: 1px solid rgba(255,255,255,.35);
}

/* Optional: smaller badge on narrow screens */
@media (max-width: 480px) {
  .mm-calendar-badge { width: 50px; height: 58px; }
  .mm-cal-header { font-size: 11px; padding: 5px 0; }
  .mm-cal-day { font-size: 20px; }
}
</style>

# Upcoming Concerts

{% include feature_row %}



