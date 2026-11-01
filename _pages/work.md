---
layout: page
title: Work
description: Research and interactive systems in accessibility, human–AI interaction, and XR.
permalink: /work/
nav: true
nav_order: 2
---

<style>
  .work-tabs { margin-top: 1.4rem; }
  .work-tab-bar { display: flex; flex-wrap: wrap; gap: .55rem; padding-bottom: 1rem; border-bottom: 1px solid var(--global-divider-color); }
  .work-tab { border: 1px solid var(--global-divider-color); border-radius: 999px; padding: .52rem 1rem; background: transparent; color: var(--global-text-color); cursor: pointer; font: inherit; font-size: .92rem; transition: background .15s ease, color .15s ease, border-color .15s ease; }
  .work-tab:hover, .work-tab:focus-visible { border-color: var(--global-theme-color); outline-offset: 3px; }
  .work-tab[aria-selected="true"] { background: var(--global-theme-color); border-color: var(--global-theme-color); color: var(--global-bg-color); }
  .work-panel { padding-top: 1.5rem; }
  .work-panel[hidden] { display: none !important; }
  .work-panel-intro { color: var(--global-text-color-light); margin-bottom: 1.25rem; }
  .work-list { margin: 0; padding: 0; list-style: none; }
  .work-list-item { border-bottom: 1px solid var(--global-divider-color); }
  .work-list-link { display: flex; justify-content: space-between; align-items: center; gap: 1.5rem; padding: 1.15rem 0; color: var(--global-text-color); text-decoration: none !important; }
  .work-list-title { display: block; font-size: 1.1rem; font-weight: 600; line-height: 1.45; }
  .work-list-description { display: block; margin-top: .3rem; font-size: .94rem; line-height: 1.6; color: var(--global-text-color-light); }
  .work-list-arrow { flex: 0 0 auto; font-size: 1.15rem; color: var(--global-text-color-light); }
  .work-list-link:hover .work-list-title, .work-list-link:focus-visible .work-list-title { color: var(--global-theme-color); }
  @media (max-width: 540px) { .work-tab { padding: .46rem .7rem; font-size: .83rem; } .work-list-link { gap: .7rem; } }
</style>

<div class="work-tabs" id="work-tabs">
  <div class="work-tab-bar" role="tablist" aria-label="Work categories">
    <button type="button" class="work-tab" role="tab" id="tab-research" aria-controls="panel-research" aria-selected="true" tabindex="0" data-work-tab="research">Research</button>
    <button type="button" class="work-tab" role="tab" id="tab-research-engineering" aria-controls="panel-research-engineering" aria-selected="false" tabindex="-1" data-work-tab="research-engineering">Research Engineering</button>
    <button type="button" class="work-tab" role="tab" id="tab-undergraduate" aria-controls="panel-undergraduate" aria-selected="false" tabindex="-1" data-work-tab="undergraduate">Undergraduate Projects</button>
  </div>

  {% assign work_categories = 'research,research-engineering,undergraduate' | split: ',' %}
  {% for category in work_categories %}
    {% assign work_items = site.projects | where: 'category', category | sort: 'importance' %}
    <section class="work-panel" id="panel-{{ category }}" role="tabpanel" aria-labelledby="tab-{{ category }}" {% unless forloop.first %}hidden{% endunless %}>
      {% if category == 'research' %}
        <p class="work-panel-intro">Research on accessibility, human–AI interaction, and XR.</p>
      {% elsif category == 'research-engineering' %}
        <p class="work-panel-intro">Interactive systems and experimental infrastructure developed for research.</p>
      {% else %}
        <p class="work-panel-intro">Selected projects from my undergraduate studies.</p>
      {% endif %}
      <ul class="work-list">
        {% for project in work_items %}
          <li class="work-list-item">
            <a class="work-list-link" href="{{ project.url | relative_url }}">
              <span>
                <span class="work-list-title">{{ project.title | escape }}</span>
                {% if project.description %}<span class="work-list-description">{{ project.description | escape }}</span>{% endif %}
              </span>
              <span class="work-list-arrow" aria-hidden="true">↗</span>
            </a>
          </li>
        {% endfor %}
      </ul>
    </section>
  {% endfor %}
</div>

<script>
  (function () {
    const root = document.getElementById('work-tabs');
    if (!root) return;
    const tabs = Array.from(root.querySelectorAll('[data-work-tab]'));
    const valid = tabs.map((tab) => tab.dataset.workTab);

    function activate(category, focus) {
      if (!valid.includes(category)) return;
      tabs.forEach((tab) => {
        const selected = tab.dataset.workTab === category;
        tab.setAttribute('aria-selected', String(selected));
        tab.tabIndex = selected ? 0 : -1;
        const panel = document.getElementById(tab.getAttribute('aria-controls'));
        if (panel) panel.hidden = !selected;
        if (selected && focus) tab.focus();
      });
    }

    tabs.forEach((tab, index) => {
      tab.addEventListener('click', () => activate(tab.dataset.workTab, false));
      tab.addEventListener('keydown', (event) => {
        if (!['ArrowRight', 'ArrowLeft', 'Home', 'End'].includes(event.key)) return;
        event.preventDefault();
        let next = index;
        if (event.key === 'ArrowRight') next = (index + 1) % tabs.length;
        if (event.key === 'ArrowLeft') next = (index - 1 + tabs.length) % tabs.length;
        if (event.key === 'Home') next = 0;
        if (event.key === 'End') next = tabs.length - 1;
        activate(tabs[next].dataset.workTab, true);
      });
    });
  })();
</script>
