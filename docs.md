---
layout: page
title: Documentation
permalink: /docs/
---

<div class="docs">

  <ul class="doc-list">
    {% for doc in site.docs %}
      <li>
        <h2>
          <a class="doc-link" href="{{ doc.url | prepend: site.baseurl }}">{{ doc.title }}</a>
        </h2>
      </li>
    {% endfor %}
  </ul>

</div>
