---
permalink: /concerts/
title: Concerts
layout: splash
author_profile: false
header:
  overlay_color: "#000"
  overlay_filter: "0.35" # 0–1 darkens image
  overlay_image: /assets/sandstone.jpg

# Row A
feature_row_a:
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
    badge_date: 2025-11-04   # ← ISO date (auto-formats to NOV / 3)

  - image_path: /assets/concert_images/candlelight.jpg
    # alt: "Media"
    title: |
      Candlelight Concert:  
      Rock Classics 
    excerpt: "Santa Fe"
    url: https://feverup.com/m/369543
    btn_label: "Tickets / More Info"
    btn_class: "btn--primary"
    badge_month: NOV          # ← manual
    badge_day: 22

  - image_path: /assets/concert_images/candlelight.jpg
    # alt: "Studio"
    title: |
      Candlelight Concert:  
      Coldplay x Imagine Dragons 
    excerpt: "Santa Fe"
    url: https://feverup.com/m/369545
    btn_label: "Tickets / More Info"
    btn_class: "btn--primary"
    badge_month: NOV          # ← manual
    badge_day: 22

# Row B
feature_row_b:
  - image_path: /assets/concert_images/wcm_recital_hall.png
    # alt: "Performances"
    title: "Prometheus Trio Concert (Milwaukee)"
    excerpt: |
          Martinu Piano Quartet
          Dvorak “Dumky” Piano Trio  
          Stefanie Jacob, piano  
          Scott Tisdel, cello  
          Emmy Tisdel Lohr, violin 
    url: https://emmy-tisdel.com/concerts/
    btn_label: "Tickets / More Info"
    badge_month: DEC        
    badge_day: 8

  - image_path: /assets/concert_images/wcm_recital_hall.png
    # alt: "Media"
    title: "Pro Musica Winter Orchestra Concert (Santa Fe)"
    excerpt: |
          Mozart Symphony No. 36  
          Mozart Violin Concerto No. 5  
          Mozart Piano Concerto No. 24  
    url: https://tickets.sfpromusica.org/10605/10607?_gl=1*1m8y5bz*_ga*NzM0MTgwNTkyLjE3NjEyNTQ4OTA.*_ga_7PNM7QVG5Q*czE3NjEyNTQ4OTAkbzEkZzEkdDE3NjEyNTQ5MzYkajE0JGwwJGgw*_ga_15GGZ9BZ4L*czE3NjEyNTQ4OTAkbzEkZzEkdDE3NjEyNTQ5MzYkajE0JGwwJGgw
    btn_label: "Tickets / More Info"
    btn_class: "btn--primary"
    badge_month: JAN       
    badge_day: 25

  - image_path: /assets/concert_images/wcm_recital_hall.png
    # alt: "Studio"
    title: "Shorewood Chamber Orchestra (Milwaukee)"
    excerpt: |
          Beethoven Triple Concerto  
          Karen Frink, conductor    
          Stefanie Jacob, piano  
          Scott Tisdel, cello  
          Emmy Tisdel Lohr, violin 
    url: https://emmy-tisdel.com/concerts/
    btn_label: "Tickets / More Info"
    btn_class: "btn--primary"
    badge_month: FEB          # ← manual
    badge_day: 10
---

# Upcoming Concerts

<div id="row-a">
  {% include feature_row id="feature_row_a" %}
</div>

<div id="row-b" style="margin-top: 2rem;">
  {% include feature_row id="feature_row_b" %}
</div>

<script>
function attachCalendarBadges(wrapperSelector, dates, urls) {
  const teasers = document.querySelectorAll(wrapperSelector + ' .feature__item .archive__item-teaser');
  teasers.forEach(function (teaser, i) {
    const d = dates[i];
    if (!d || !d.month || !d.day) return;

    // Anchor badge to image container
    if (getComputedStyle(teaser).position === 'static') {
      teaser.style.position = 'relative';
    }

    const linkUrl = urls && urls[i];
    const wrapper = linkUrl ? document.createElement('a') : document.createElement('span');
    if (linkUrl) { wrapper.href = linkUrl; wrapper.style.textDecoration = 'none'; }

    const badge = document.createElement('span');
    badge.setAttribute('aria-label', 'Event date');

    // Inline styles (ensures overlay even if site CSS differs)
    const b = badge.style;
    b.position = 'absolute';
    b.top = '-44px';            // ← top-right
    b.right = '5px';
    // b.width = '58px';
    // b.height = '64px';
    b.width = '80px';
    b.height = '88px';
    b.borderRadius = '10px';
    b.overflow = 'hidden';
    b.display = 'inline-flex';
    b.flexDirection = 'column';
    b.alignItems = 'center';
    b.justifyContent = 'stretch';
    b.boxShadow = '0 2px 6px rgba(0,0,0,.28)';
    b.zIndex = '30';
    b.border = '1px solid rgba(255,255,255,.35)';

    const header = document.createElement('span');
    Object.assign(header.style, {
      background: '#e63946', color: '#fff', fontWeight: '700',
      fontSize: '16px', letterSpacing: '0.5px', textTransform: 'uppercase',
      lineHeight: '1', padding: '6px 0', width: '100%', textAlign: 'center'
    });
    header.textContent = d.month;

    const day = document.createElement('span');
    Object.assign(day.style, {
      background: '#fff', color: '#111', fontWeight: '800',
      fontSize: '28px', lineHeight: '1', flex: '1 1 auto', display: 'flex',
      alignItems: 'center', justifyContent: 'center', width: '100%'
    });
    day.textContent = d.day;

    badge.appendChild(header);
    badge.appendChild(day);
    wrapper.appendChild(badge);
    teaser.appendChild(wrapper);
  });
}

document.addEventListener('DOMContentLoaded', function () {
  // Build data for Row A
  const datesA = [
    {% for f in page.feature_row_a %}
      {% if f.badge_date %}
        { month: "{{ f.badge_date | date: '%b' | upcase }}", day: "{{ f.badge_date | date: '%-d' }}" },
      {% elsif f.badge_month or f.badge_day %}
        { month: "{{ f.badge_month }}", day: "{{ f.badge_day }}" },
      {% else %} null,
      {% endif %}
    {% endfor %}
  ];
  const urlsA = [
    {% for f in page.feature_row_a %} {{ f.url | jsonify }}, {% endfor %}
  ];
  attachCalendarBadges('#row-a', datesA, urlsA);

  // Build data for Row B
  const datesB = [
    {% for f in page.feature_row_b %}
      {% if f.badge_date %}
        { month: "{{ f.badge_date | date: '%b' | upcase }}", day: "{{ f.badge_date | date: '%-d' }}" },
      {% elsif f.badge_month or f.badge_day %}
        { month: "{{ f.badge_month }}", day: "{{ f.badge_day }}" },
      {% else %} null,
      {% endif %}
    {% endfor %}
  ];
  const urlsB = [
    {% for f in page.feature_row_b %} {{ f.url | jsonify }}, {% endfor %}
  ];
  attachCalendarBadges('#row-b', datesB, urlsB);

  // Add more rows by repeating the pattern:
  // const datesC = [ ...from page.feature_row_c... ];
  // const urlsC =  [ ...from page.feature_row_c... ];
  // attachCalendarBadges('#row-c', datesC, urlsC);
});
</script>



