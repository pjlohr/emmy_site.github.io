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

# Upcoming Concerts

{% include feature_row %}

<div id="concert-row">
  {% include feature_row %}
</div>

<script>
document.addEventListener('DOMContentLoaded', function () {
  // Build per-tile date data from front matter (Liquid → JS)
  const dates = [
    {% for f in page.feature_row %}
      {% if f.badge_date %}
        { month: "{{ f.badge_date | date: '%b' | upcase }}", day: "{{ f.badge_date | date: '%-d' }}" },
      {% elsif f.badge_month or f.badge_day %}
        { month: "{{ f.badge_month }}", day: "{{ f.badge_day }}" },
      {% else %}
        null,
      {% endif %}
    {% endfor %}
  ];

  // Optional: URLs if you want the badge clickable
  const urls = [
    {% for f in page.feature_row %}
      {{ f.url | jsonify }},
    {% endfor %}
  ];

  // Find the teaser containers inside this specific row
  const teasers = document.querySelectorAll('#concert-row .feature__item .archive__item-teaser');

  teasers.forEach(function (teaser, i) {
    const d = dates[i];
    if (!d || !d.month || !d.day) return;

    // Ensure the badge anchors to the image container
    const cs = window.getComputedStyle(teaser);
    if (cs.position === 'static') {
      teaser.style.position = 'relative';
    }

    // Create badge (inline styles so it overlays even without CSS)
    const badge = document.createElement('span');
    badge.setAttribute('aria-label', 'Event date');

    // If you want the badge to be clickable, wrap in <a>
    const linkUrl = urls[i];
    const wrapper = linkUrl ? document.createElement('a') : document.createElement('span');
    if (linkUrl) {
      wrapper.href = linkUrl;
      wrapper.style.textDecoration = 'none';
    }

    // Badge container styles (calendar card)
    const b = badge.style;
    b.position = 'absolute';
    b.top = '10px';
    b.right = '10px';
    b.width = '58px';
    b.height = '64px';
    b.borderRadius = '10px';
    b.overflow = 'hidden';
    b.display = 'inline-flex';
    b.flexDirection = 'column';
    b.alignItems = 'center';
    b.justifyContent = 'stretch';
    b.boxShadow = '0 2px 6px rgba(0,0,0,.28)';
    b.zIndex = '30';
    b.border = '1px solid rgba(255,255,255,.35)';
    b.pointerEvents = 'auto'; // keep clickable if wrapped in <a>

    // Month header
    const header = document.createElement('span');
    const h = header.style;
    h.background = '#e63946';
    h.color = '#fff';
    h.fontWeight = '700';
    h.fontSize = '12px';
    h.letterSpacing = '0.5px';
    h.textTransform = 'uppercase';
    h.lineHeight = '1';
    h.padding = '6px 0';
    h.width = '100%';
    h.textAlign = 'center';
    header.textContent = d.month;

    // Day body
    const day = document.createElement('span');
    const dy = day.style;
    dy.background = '#fff';
    dy.color = '#111';
    dy.fontWeight = '800';
    dy.fontSize = '22px';
    dy.lineHeight = '1';
    dy.flex = '1 1 auto';
    dy.display = 'flex';
    dy.alignItems = 'center';
    dy.justifyContent = 'center';
    dy.width = '100%';
    day.textContent = d.day;

    badge.appendChild(header);
    badge.appendChild(day);
    wrapper.appendChild(badge);
    teaser.appendChild(wrapper);
  });
});
</script>


<!-- <script>
document.addEventListener('DOMContentLoaded', function () {
  // Build an array of date objects (or null) from front matter
  const dates = [
    {% for f in page.feature_row %}
      {% if f.badge_date %}
        { month: "{{ f.badge_date | date: '%b' | upcase }}", day: "{{ f.badge_date | date: '%-d' }}" },
      {% elsif f.badge_month or f.badge_day %}
        { month: "{{ f.badge_month }}", day: "{{ f.badge_day }}" },
      {% else %}
        null,
      {% endif %}
    {% endfor %}
  ];

  // Find each feature tile's teaser image container and inject the badge
  const teasers = document.querySelectorAll('.feature__item .archive__item-teaser');
  teasers.forEach(function (teaser, i) {
    const d = dates[i];
    if (!d || !d.month || !d.day) return;

    const badge = document.createElement('span');
    badge.className = 'mm-calendar-badge';
    badge.innerHTML = '<span class="mm-cal-header">' + d.month + '</span>' +
                      '<span class="mm-cal-day">' + d.day + '</span>';
    // Ensure anchoring and add to DOM
    teaser.style.position = 'relative';
    teaser.appendChild(badge);
  });
});
</script> -->