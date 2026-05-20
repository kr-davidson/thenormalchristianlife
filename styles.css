/* ============================================================
   THE NORMAL CHRISTIAN LIFE — Guided Study Microsite
   script.js — Shared JavaScript
   ============================================================ */

(function () {
  'use strict';

  /* ----------------------------------------------------------
     MOBILE NAVIGATION TOGGLE
  ---------------------------------------------------------- */
  function initMobileNav() {
    var toggle = document.querySelector('.nav-toggle');
    var nav    = document.querySelector('.site-nav');
    if (!toggle || !nav) return;

    toggle.addEventListener('click', function () {
      var isOpen = nav.classList.toggle('open');
      toggle.setAttribute('aria-expanded', String(isOpen));
    });

    // Close when a nav link is clicked
    nav.querySelectorAll('a').forEach(function (link) {
      link.addEventListener('click', function () {
        nav.classList.remove('open');
        toggle.setAttribute('aria-expanded', 'false');
      });
    });
  }

  /* ----------------------------------------------------------
     ACTIVE LINK HIGHLIGHTING
     Marks the nav link whose href matches the current page.
  ---------------------------------------------------------- */
  function initActiveLinks() {
    var current = window.location.pathname.split('/').pop() || 'index.html';
    document.querySelectorAll('.site-nav a').forEach(function (link) {
      var href = link.getAttribute('href') || '';
      var page = href.split('/').pop();
      if (page === current) {
        link.classList.add('active');
        link.setAttribute('aria-current', 'page');
      }
    });
  }

  /* ----------------------------------------------------------
     SMOOTH SCROLLING
     Intercepts in-page anchor clicks and scrolls smoothly.
  ---------------------------------------------------------- */
  function initSmoothScroll() {
    document.querySelectorAll('a[href^="#"]').forEach(function (anchor) {
      anchor.addEventListener('click', function (e) {
        var target = document.querySelector(this.getAttribute('href'));
        if (target) {
          e.preventDefault();
          target.scrollIntoView({ behavior: 'smooth' });
        }
      });
    });
  }

  /* ----------------------------------------------------------
     READING PROGRESS BAR (chapter pages only)
  ---------------------------------------------------------- */
  function initProgressBar() {
    var bar = document.getElementById('progress-bar');
    if (!bar) return;

    function update() {
      var scrollTop  = window.scrollY || document.documentElement.scrollTop;
      var docHeight  = document.documentElement.scrollHeight - document.documentElement.clientHeight;
      var pct = docHeight > 0 ? (scrollTop / docHeight) * 100 : 0;
      bar.style.width = pct + '%';
    }

    window.addEventListener('scroll', update, { passive: true });
    update();
  }

  /* ----------------------------------------------------------
     BACK TO TOP BUTTON
  ---------------------------------------------------------- */
  function initBackTop() {
    var btn = document.getElementById('back-top');
    if (!btn) return;

    function updateVisibility() {
      btn.classList.toggle('visible', window.scrollY > 400);
    }

    btn.addEventListener('click', function () {
      window.scrollTo({ top: 0, behavior: 'smooth' });
    });

    window.addEventListener('scroll', updateVisibility, { passive: true });
    updateVisibility();
  }

  /* ----------------------------------------------------------
     FLOATING TABLE OF CONTENTS DOTS
  ---------------------------------------------------------- */
  function initTocDots() {
    var dots     = document.querySelectorAll('.toc-dot');
    if (!dots.length) return;

    var sections = Array.from(dots).map(function (d) {
      return document.getElementById(d.dataset.target);
    }).filter(Boolean);

    dots.forEach(function (dot) {
      dot.addEventListener('click', function () {
        var target = document.getElementById(dot.dataset.target);
        if (target) target.scrollIntoView({ behavior: 'smooth' });
      });
    });

    function updateActive() {
      var activeIndex = 0;
      sections.forEach(function (sec, i) {
        if (sec && sec.getBoundingClientRect().top < window.innerHeight * 0.45) {
          activeIndex = i;
        }
      });
      dots.forEach(function (d, i) {
        d.classList.toggle('active', i === activeIndex);
      });
    }

    window.addEventListener('scroll', updateActive, { passive: true });
    updateActive();
  }

  /* ----------------------------------------------------------
     COLLAPSIBLE SECTIONS
  ---------------------------------------------------------- */
  function initCollapsible() {
    document.querySelectorAll('.collapsible-btn').forEach(function (btn) {
      btn.addEventListener('click', function () {
        var bodyId = btn.dataset.section;
        var body   = document.getElementById(bodyId);
        if (!body) return;
        var isOpen = btn.classList.contains('open');
        btn.classList.toggle('open', !isOpen);
        btn.setAttribute('aria-expanded', String(!isOpen));
        body.classList.toggle('open', !isOpen);
      });
    });
  }

  /* ----------------------------------------------------------
     MARK AS COMPLETE (local storage, chapter pages only)
     Adds a simple toggle so readers can track their progress.
  ---------------------------------------------------------- */
  function initMarkComplete() {
    var btn = document.getElementById('mark-complete');
    if (!btn) return;

    var key       = 'ncl-complete-' + (btn.dataset.chapter || 'unknown');
    var isComplete = localStorage.getItem(key) === 'true';

    function render(complete) {
      btn.textContent = complete ? '&#10003; Marked Complete' : 'Mark as Complete';
      btn.classList.toggle('complete', complete);
    }

    render(isComplete);

    btn.addEventListener('click', function () {
      isComplete = !isComplete;
      localStorage.setItem(key, String(isComplete));
      render(isComplete);
    });
  }

  /* ----------------------------------------------------------
     HOMEPAGE: update chapter card states from local storage
  ---------------------------------------------------------- */
  function initChapterCardStates() {
    document.querySelectorAll('.chapter-card[data-chapter]').forEach(function (card) {
      var key       = 'ncl-complete-' + card.dataset.chapter;
      var isComplete = localStorage.getItem(key) === 'true';
      if (isComplete) {
        var badge = card.querySelector('.card-badge');
        if (badge) {
          badge.textContent = 'Complete';
          badge.className   = 'card-badge badge-complete';
        }
      }
    });
  }

  /* ----------------------------------------------------------
     INIT
  ---------------------------------------------------------- */
  document.addEventListener('DOMContentLoaded', function () {
    initMobileNav();
    initActiveLinks();
    initSmoothScroll();
    initProgressBar();
    initBackTop();
    initTocDots();
    initCollapsible();
    initMarkComplete();
    initChapterCardStates();
  });

}());
