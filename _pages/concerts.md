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
    title: "Candlelight Concert"
    excerpt: |
      Rock Classics  
      Santa Fe 
    url: https://feverup.com/m/369543
    btn_label: "Tickets / More Info"
    btn_class: "btn--primary"
    badge_month: NOV          # ← manual
    badge_day: 22

  - image_path: /assets/concert_images/candlelight.jpg
    # alt: "Studio"
    title: "Candlelight Concert"
    excerpt: |
      Coldplay x Imagine Dragons  
      Santa Fe 
    url: https://feverup.com/m/369545
    btn_label: "Tickets / More Info"
    btn_class: "btn--primary"
    badge_month: NOV          # ← manual
    badge_day: 22

# Row B
# feature_row_b:
#   - image_path: "{{ '/assets/concert_images/candlelight.jpg' | relative_url }}"
#     title: "Candlelight: Coldplay x Imagine Dragons"
#     excerpt: "Santa Fe"
#     url: https://example.com/c
#     btn_label: "Tickets"
#     btn_class: "btn--primary"
#     badge_date: 2025-12-12
---

# Upcoming Concerts

<div id="row-a">
  {% include feature_row id="feature_row_a" %}
</div>

<!-- ## Past / Other Programs
<div id="row-b" style="margin-top: 2rem;">
  {% include feature_row id="feature_row_b" %}
</div> -->

<script>
/** Percent-scaled calendar badge pinned to the image's true top-right */
function attachCalendarBadges(wrapperSelector, dates, urls) {
  // % knobs (tweak for taste)
  const INSET_X = 0.02;     // 2% of image width from the right
  const INSET_Y = 0.02;     // 2% of image height from the top
  const BADGE_W_FRAC = 0.18;   // badge width = 18% of image width
  const BADGE_MIN_W = 46;      // px clamp
  const BADGE_MAX_W = 88;      // px clamp
  const BADGE_ASPECT = 64 / 58; // height/width

  const teasers = document.querySelectorAll(
    wrapperSelector + ' .feature__item .archive__item-teaser'
  );

  function placeBadge(teaser, img, wrapper, badge) {
    if (getComputedStyle(teaser).position === 'static') teaser.style.position = 'relative';

    // Attach (hidden) to measure
    badge.style.visibility = 'hidden';
    teaser.appendChild(wrapper);

    const tRect = teaser.getBoundingClientRect();
    const iRect = img.getBoundingClientRect();
    const imgW = iRect.width;
    const imgH = iRect.height;

    // Size from image
    const badgeW = Math.max(BADGE_MIN_W, Math.min(BADGE_MAX_W, imgW * BADGE_W_FRAC));
    const badgeH = badgeW * BADGE_ASPECT;
    badge.style.width = badgeW + 'px';
    badge.style.height = badgeH + 'px';

    // Inset from image corner
    const insetX = imgW * INSET_X;
    const insetY = imgH * INSET_Y;

    // Top-right of image relative to teaser
    const top  = (iRect.top  - tRect.top) + insetY;
    const left = (iRect.right - tRect.left) - insetX - badgeW;

    Object.assign(badge.style, {
      position: 'absolute',
      top: top + 'px',
      left: left + 'px',
      visibility: 'visible',
      zIndex: 50
    });
  }

  teasers.forEach(function (teaser, i) {
    const d = dates[i];
    if (!d || !d.month || !d.day) return;

    const img = teaser.querySelector('img');
    if (!img) return;

    const linkUrl = urls && urls[i];
    const wrapper = linkUrl ? document.createElement('a') : document.createElement('span');
    if (linkUrl) { wrapper.href = linkUrl; wrapper.style.textDecoration = 'none'; }

    // Build badge
    const badge = document.createElement('span');
    badge.setAttribute('aria-label', 'Event date');
    Object.assign(badge.style, {
      borderRadius: '10px',
      overflow: 'hidden',
      display: 'inline-flex',
      flexDirection: 'column',
      alignItems: 'center',
      justifyContent: 'stretch',
      boxShadow: '0 2px 6px rgba(0,0,0,.28)',
      border: '1px solid rgba(255,255,255,.35)',
      background: 'transparent'
    });

    const header = document.createElement('span');
    Object.assign(header.style, {
      background: '#e63946', color: '#fff', fontWeight: '700',
      fontSize: '12px', letterSpacing: '0.5px', textTransform: 'uppercase',
      lineHeight: '1', padding: '6px 0', width: '100%', textAlign: 'center'
    });
    header.textContent = d.month;

    const day = document.createElement('span');
    Object.assign(day.style, {
      background: '#fff', color: '#111', fontWeight: '800',
      fontSize: '22px', lineHeight: '1', flex: '1 1 auto', display: 'flex',
      alignItems: 'center', justifyContent: 'center', width: '100%'
    });
    day.textContent = d.day;

    badge.appendChild(header);
    badge.appendChild(day);
    wrapper.appendChild(badge);

    const tryPlace = () => requestAnimationFrame(() => placeBadge(teaser, img, wrapper, badge));
    if (img.complete && img.naturalWidth) tryPlace();
    else img.addEventListener('load', tryPlace, { once: true });

    window.addEventListener('resize', tryPlace);
  });
}

/* ---- Auto-detect rows present in front matter and attach ---- */
document.addEventListener('DOMContentLoaded', function () {
  // Helper to attach for one row (suffix like 'a','b','c')
  function bindRow(suffix, selector) {
    // Build dates/urls arrays from Liquid only if the row exists
    {% if page.feature_row_a %} if (suffix === 'a') {
      const dates = [
        {% for f in page.feature_row_a %}
          {% if f.badge_date %}
            { month: "{{ f.badge_date | date: '%b' | upcase }}", day: "{{ f.badge_date | date: '%-d' }}" },
          {% elsif f.badge_month or f.badge_day %}
            { month: "{{ f.badge_month }}", day: "{{ f.badge_day }}" },
          {% else %} null,
          {% endif %}
        {% endfor %}
      ];
      const urls  = [{% for f in page.feature_row_a %} {{ f.url | jsonify }}, {% endfor %}];
      attachCalendarBadges(selector, dates, urls);
    } {% endif %}

    {% if page.feature_row_b %} if (suffix === 'b') {
      const dates = [
        {% for f in page.feature_row_b %}
          {% if f.badge_date %}
            { month: "{{ f.badge_date | date: '%b' | upcase }}", day: "{{ f.badge_date | date: '%-d' }}" },
          {% elsif f.badge_month or f.badge_day %}
            { month: "{{ f.badge_month }}", day: "{{ f.badge_day }}" },
          {% else %} null,
          {% endif %}
        {% endfor %}
      ];
      const urls  = [{% for f in page.feature_row_b %} {{ f.url | jsonify }}, {% endfor %}];
      attachCalendarBadges(selector, dates, urls);
    } {% endif %}

    {% if page.feature_row_c %} if (suffix === 'c') {
      const dates = [
        {% for f in page.feature_row_c %}
          {% if f.badge_date %}
            { month: "{{ f.badge_date | date: '%b' | upcase }}", day: "{{ f.badge_date | date: '%-d' }}" },
          {% elsif f.badge_month or f.badge_day %}
            { month: "{{ f.badge_month }}", day: "{{ f.badge_day }}" },
          {% else %} null,
          {% endif %}
        {% endfor %}
      ];
      const urls  = [{% for f in page.feature_row_c %} {{ f.url | jsonify }}, {% endfor %}];
      attachCalendarBadges(selector, dates, urls);
    } {% endif %}

    {% if page.feature_row_d %} if (suffix === 'd') {
      const dates = [
        {% for f in page.feature_row_d %}
          {% if f.badge_date %}
            { month: "{{ f.badge_date | date: '%b' | upcase }}", day: "{{ f.badge_date | date: '%-d' }}" },
          {% elsif f.badge_month or f.badge_day %}
            { month: "{{ f.badge_month }}", day: "{{ f.badge_day }}" },
          {% else %} null,
          {% endif %}
        {% endfor %}
      ];
      const urls  = [{% for f in page.feature_row_d %} {{ f.url | jsonify }}, {% endfor %}];
      attachCalendarBadges(selector, dates, urls);
    } {% endif %}
  }

  // Try rows a..d (add more if you need)
  bindRow('a', '#row-a');
  bindRow('b', '#row-b');
  bindRow('c', '#row-c');
  bindRow('d', '#row-d');
});





</script>





<!-- <script>
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
    b.top = '-100px';            // ← top-right
    b.right = '5px';
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

    const header = document.createElement('span');
    Object.assign(header.style, {
      background: '#e63946', color: '#fff', fontWeight: '700',
      fontSize: '12px', letterSpacing: '0.5px', textTransform: 'uppercase',
      lineHeight: '1', padding: '6px 0', width: '100%', textAlign: 'center'
    });
    header.textContent = d.month;

    const day = document.createElement('span');
    Object.assign(day.style, {
      background: '#fff', color: '#111', fontWeight: '800',
      fontSize: '22px', lineHeight: '1', flex: '1 1 auto', display: 'flex',
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

  // // Build data for Row B
  // const datesB = [
  //   {% for f in page.feature_row_b %}
  //     {% if f.badge_date %}
  //       { month: "{{ f.badge_date | date: '%b' | upcase }}", day: "{{ f.badge_date | date: '%-d' }}" },
  //     {% elsif f.badge_month or f.badge_day %}
  //       { month: "{{ f.badge_month }}", day: "{{ f.badge_day }}" },
  //     {% else %} null,
  //     {% endif %}
  //   {% endfor %}
  // ];
  // const urlsB = [
  //   {% for f in page.feature_row_b %} {{ f.url | jsonify }}, {% endfor %}
  // ];
  // attachCalendarBadges('#row-b', datesB, urlsB);

  // Add more rows by repeating the pattern:
  // const datesC = [ ...from page.feature_row_c... ];
  // const urlsC =  [ ...from page.feature_row_c... ];
  // attachCalendarBadges('#row-c', datesC, urlsC);
});
</script>


 -->
