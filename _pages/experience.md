---
layout: page
title: Experience
description: Employment, leadership, and community service
permalink: /experience/
nav: true
nav_order: 3
---

<style>
.experience-tabs {
  display: flex;
  flex-wrap: wrap;
  gap: 0.75rem;
  margin: 2rem 0;
}

.experience-tab {
  background: transparent;
  border: 1px solid var(--global-divider-color);
  border-radius: 8px;
  color: var(--global-text-color);
  cursor: pointer;
  font-size: 0.95rem;
  padding: 0.65rem 1.1rem;
  transition: all 0.2s ease;
}

.experience-tab:hover {
  border-color: var(--global-theme-color);
  color: var(--global-theme-color);
}

.experience-tab.active {
  background: var(--global-theme-color);
  border-color: var(--global-theme-color);
  color: white;
}

.experience-panel[hidden] {
  display: none;
}

.experience-item {
  padding: 1.5rem 0;
  border-bottom: 1px solid var(--global-divider-color);
}

.experience-item:last-child {
  border-bottom: none;
}

.experience-item h3 {
  font-size: 1.15rem;
  font-weight: 600;
  margin-bottom: 0.35rem;
}

.experience-org {
  font-size: 0.95rem;
  margin-bottom: 0.25rem;
}

.experience-date {
  color: var(--global-text-color-light);
  font-size: 0.85rem;
  margin-bottom: 0.75rem;
}

.experience-description {
  font-size: 0.95rem;
  line-height: 1.75;
  margin-bottom: 0;
}

.experience-roles {
  margin-top: 0.75rem;
  padding-left: 1.25rem;
  line-height: 1.8;
}

.experience-roles li {
  margin-bottom: 0.25rem;
}
</style>

<div class="experience-tabs" role="tablist" aria-label="Experience categories">
  <button class="experience-tab active" id="tab-employment" type="button"
    role="tab" aria-selected="true" aria-controls="panel-employment"
    data-tab="employment">
    Employment
  </button>

  <button class="experience-tab" id="tab-leadership" type="button"
    role="tab" aria-selected="false" aria-controls="panel-leadership"
    data-tab="leadership" tabindex="-1">
    Leadership
  </button>

  <button class="experience-tab" id="tab-service" type="button"
    role="tab" aria-selected="false" aria-controls="panel-service"
    data-tab="service" tabindex="-1">
    Community &amp; Service
  </button>
</div>

<!-- EMPLOYMENT -->

<section class="experience-panel" id="panel-employment"
  role="tabpanel" aria-labelledby="tab-employment">

  <div class="experience-item">
    <h3>Departmental Assistant &amp; Laboratory Safety Officer</h3>
    <div class="experience-org">
      Ewha Womans University, Department of Biology Education
    </div>
    <div class="experience-date">
      Sep 2025 – Present (Expected completion: Feb 2027)
    </div>
    <p class="experience-description">
      Responsible for departmental administrative tasks and
      laboratory safety management.
    </p>
  </div>

  <div class="experience-item">
    <h3>English Instructor</h3>
    <div class="experience-org">
      E.K.조진원 영어학원
    </div>
    <div class="experience-date">
      Dec 2022 – Aug 2023
    </div>
    <p class="experience-description">
      Independently taught English classes and supported
      students' English language learning.
    </p>
  </div>

</section>

<!-- LEADERSHIP -->

<section class="experience-panel" id="panel-leadership"
  role="tabpanel" aria-labelledby="tab-leadership" hidden>

  <div class="experience-item">
    <h3>XREAL — XR Academic Society</h3>
    <div class="experience-org">
      Ewha Womans University
    </div>
    <div class="experience-date">
      Sep 2024 – Present
    </div>

    <ul class="experience-roles">
      <li><strong>7th Cohort:</strong> Junior Member</li>
      <li><strong>8th Cohort:</strong> Vice Head of Research</li>
      <li><strong>9th Cohort:</strong> Vice President</li>
      <li><strong>10th–11th Cohorts:</strong> Exhibition Operations Support</li>
    </ul>

    <p class="experience-description">
      Contributed to XR academic society activities, research
      leadership, and organizational operations. Facilitated
      connections with an external university professor and
      supported gallery exhibition operations.
    </p>
  </div>

</section>

<!-- COMMUNITY & SERVICE -->

<section class="experience-panel" id="panel-service"
  role="tabpanel" aria-labelledby="tab-service" hidden>

  <div class="experience-item">
    <h3>Student Volunteer</h3>
    <div class="experience-org">
      SIGCHI Korea Local Chapter
    </div>
    <div class="experience-date">
      2026
    </div>
    <p class="experience-description">
      Supported academic community events and their operations.
    </p>
  </div>

  <div class="experience-item">
    <h3>Museum Docent</h3>
    <div class="experience-date">
      Feb 2026 – Jul 2026
    </div>
    <p class="experience-description">
      Provided exhibition interpretation and engaged with
      museum visitors.
    </p>
  </div>

  <div class="experience-item">
    <h3>Engineering Mentor</h3>
    <div class="experience-org">
      WISET — Women in Engineering Research Team
    </div>
    <div class="experience-date">
      2025
    </div>
    <p class="experience-description">
      Mentored female high school students interested in
      engineering. Taught Unity development, introduced
      students to research activities, and shared information
      about engineering education and university life.
    </p>
  </div>

</section>

<script>
(function () {
  const tabs = Array.from(
    document.querySelectorAll(".experience-tab")
  );
  const panels = Array.from(
    document.querySelectorAll(".experience-panel")
  );

  function activateTab(tab, moveFocus = false) {
    const target = "panel-" + tab.dataset.tab;

    tabs.forEach(function (item) {
      const active = item === tab;
      item.classList.toggle("active", active);
      item.setAttribute("aria-selected", String(active));
      item.tabIndex = active ? 0 : -1;
    });

    panels.forEach(function (panel) {
      panel.hidden = panel.id !== target;
    });

    if (moveFocus) tab.focus();
  }

  tabs.forEach(function (tab, index) {
    tab.addEventListener("click", function () {
      activateTab(tab);
    });

    tab.addEventListener("keydown", function (event) {
      let next = index;

      if (event.key === "ArrowRight") {
        next = (index + 1) % tabs.length;
      } else if (event.key === "ArrowLeft") {
        next = (index - 1 + tabs.length) % tabs.length;
      } else if (event.key === "Home") {
        next = 0;
      } else if (event.key === "End") {
        next = tabs.length - 1;
      } else {
        return;
      }

      event.preventDefault();
      activateTab(tabs[next], true);
    });
  });
})();
</script>
