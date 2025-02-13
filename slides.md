---
# You can also start simply with 'default'
theme: the-unnamed
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
# background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: Run your tests against Django's main!
info: |
  ## Run your tests against Django's `main`!

  Talk given at the Django London Meetup (2025-02-13). Made with [Slidev](https://sli.dev).
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
---

# Run your tests against Django's `main`!

<div>

Django London Meetup

Thursday, 13 February 2025

</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
transition: slide-left
---

# About me

- Sage Abdullah
- Developer at Torchbox
- Wagtail CMS core team member
- Google Summer of Code contributor and mentor for Wagtail and Django
- Djangonauts Space navigator

<style>
  li {
    font-size: 1.5rem;
    line-spacing: 2;
  }
</style>

---
transition: slide-left
---

# Django is **stable**

https://docs.djangoproject.com/en/stable/misc/api-stability/

> _Django is committed to API stability and forwards-compatibility._

> ... _making API stability a very high priority_ ...

> _Our aim is to provide a modern, dependable web framework of the highest quality that encourages best practices in all projects that use it._

---
transition: slide-left
---

# How to keep it stable?

<img class="mx-auto h-xs" src="/djangoci-tests.png" alt="17989 tests in Django 5.2" />

<v-click>

Also, deprecation of public APIs are done over at least two feature releases.

</v-click>

---
transition: none
---

# Django's release process

```mermaid {theme: 'neutral', scale: 1}
flowchart LR
    main["active development <br> on main branch"] -- "stable/A.B.x is forked <br> (feature freeze)" --> alpha["alpha"]
    alpha -- "non-release blocking <br> bug fix freeze" --> beta["beta"]
    beta -- translation string freeze --> RC["RC"]
    RC -- no critical bugs --> final["final"]
     main:::Pine
     alpha:::Pine
     beta:::Pine
     RC:::Pine
     final:::Pine
    classDef Pine stroke-width:4px, stroke-dasharray:none, stroke:#254336, fill:#27654A, color:#FFFFFF

```

---
transition: none
---

# Django's release process

<img class="mx-auto h-sm" src="/django-release-timeline.png" alt="Django release timeline" />

---
transition: slide-left
---

# Django's release process

```mermaid {theme: 'neutral', scale: 1}
flowchart LR
    main["main"] -- "stable/A.B.x is forked <br> (feature freeze)" --> alpha["alpha"]
    alpha -- "non-release blocking <br> bug fix freeze" --> beta["beta"]
    beta -- translation string freeze --> RC["RC"]
    RC -- no critical bugs --> final["final"]
     main:::Pine
     alpha:::Pine
     beta:::Pine
     RC:::Pine
     final:::Pine
    classDef Pine stroke-width:4px, stroke-dasharray:none, stroke:#254336, fill:#27654A, color:#FFFFFF
```

When is the best time to catch bugs?

<v-clicks>

```mermaid {theme: 'neutral', scale: 1}
flowchart LR
    pr["Pull request on GitHub"] -- "right here!" --> main["main"]
     main:::Pine
     pr:::Pine
    classDef Pine stroke-width:4px, stroke-dasharray:none, stroke:#254336, fill:#27654A, color:#FFFFFF
```

<div class="flex gap-2 w-full justify-center items-center mt-4">
  <img src="/watch-django.png" alt="Watch the Django repository" class="w-lg" />
  <div class="text-4xl"> = 😵‍💫</div>
</div>

</v-clicks>

---
transition: slide-left
---

# How you can help

Run your tests against Django's `main` branch!

```yml
test:
  runs-on: ubuntu-latest
  continue-on-error: ${{ matrix.experimental }}
  strategy:
    matrix:
      include:
        - python: '3.13'
          django: 'git+https://github.com/django/django.git@main#egg=Django'
          experimental: true
  steps:
    - uses: actions/checkout@v4
    - uses: actions/setup-python@v5
      with:
        python-version: ${{ matrix.python }}
    - run: pip install -r requirements.txt
    - if: ${{ matrix.experimental }}
      run: pip install "${{ matrix.django }}"
    - run: python -Wd manage.py test
```

---
transition: slide-left
layout: center
---

# How does that help? 🤔

---
transition: none
---

# How does that help? 🤔

<img src="/fails-against-main.png" alt="A failing test against Django's main branch" />

---
transition: none
---

# How does that help? 🤔

<img class="w-3xl mx-auto" src="/django-commits-today.png" alt="Django commits from 2 hours ago that may have caused the error" />

---
transition: slide-left
---

# How does that help **you**? 🤔

<img src="/wagtail-code-usage.png" alt="Wagtail code that uses Django's internal API that just got removed" />

<v-click>

(...or, why you shouldn't use Django's internal APIs)

</v-click>

---
transition: none
---

# How does that help **Django**?

<img src="/django-tickets.png" alt="Django tickets reported by Wagtail maintainers" />

---
transition: none
---

# How does that help **Django**?

<img class="w-lg mx-auto" src="/fullclean-ticket.png" alt="An example ticket for a regression in Django" />

---
transition: slide-left
---

# How does that help **Django**?

<img src="/django-regression-fix.png" alt="The fix committed to the Django repository" />

---
transition: slide-left
layout: center
---

# Run your test against Django's `main`...

<v-click>

...and report any issues you find!

</v-click>

---
transition: slide-left
layout: cover
---

# Thank you!

https://slides.laymonage.com/tests-django-main
