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

<script>
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
</script>