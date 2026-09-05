---
layout: single
author_profile: true
read_time: false
share: false
related: false
---

{% comment %}
  The page needs an h1 for its document outline — without one the outline starts
  at the author card's h3. It is screen-reader-only because the author card
  already shows the name, and a visible duplicate looks like a mistake.

  Keep this as raw HTML. Written as a Markdown `# Wenzhuo Xu`, Jekyll adopts the
  first heading as page.title, and the theme's SEO include then renders
  "<title>Wenzhuo Xu - Wenzhuo Xu</title>" in every browser tab.
{% endcomment %}
<h1 class="screen-reader-text">Wenzhuo Xu</h1>

I build agentic and vision–language systems that reason about physical processes — how they behave, and whether a generated video or the equations printed in a document actually respect them. I am a Ph.D. candidate in Mechanical Engineering at Carnegie Mellon University (expected May 2027), and I spent summer 2026 as a Research Scientist Intern at Adobe Research. My background is in learned surrogates and neural operators for large-scale fluid simulation, which is where the physics grounding comes from: I spent four years building models that had to agree with a solver, and I now build systems that have to agree with the world.

The thread through both halves is the same — a model's claim about a physical system should be checkable, and the machinery that checks it should be something a person can read.

**Carnegie Mellon University** — advised by [Christopher McComb](https://engineering.cmu.edu/directory/bios/mccomb-christopher.html) and [Noelia Grande Gutiérrez](https://www.meche.engineering.cmu.edu/directory/bios/grande-gutierrez-noelia.html), [Department of Mechanical Engineering](https://www.meche.engineering.cmu.edu/index.html), [CMU](https://www.cmu.edu/)
{: .affiliations}

**Adobe Research** — Research Scientist Intern, summer 2026, with [Tong Sun](https://research.adobe.com/person/tong-sun/) and [Jiuxiang Gu](https://gujiuxiang.com/)
{: .affiliations}

**Labs** — [Design Research Collective](https://cmudrc.github.io/) · [BioSiMMlab](https://www.meche.engineering.cmu.edu/faculty/gutierrez-biosimm-lab.html)
{: .affiliations}

<a href="mailto:wzxu@cmu.edu">Email</a> / <a href="/cv/">CV</a> / <a href="https://scholar.google.com/citations?user=3RqGjxwAAAAJ&hl=en">Google Scholar</a> / <a href="https://github.com/WenzhuoXu">GitHub</a> / <a href="https://www.linkedin.com/in/wenzhuo-xu-174592110/">LinkedIn</a>
{: .linkrow}

## Projects

{% assign cards = site.data.projects | sort: "rank" %}
{% include project-cards.html entries=cards %}

## Recent publications

{%- comment -%}
  Strictly reverse-chronological by `date`, journals and conference papers
  together. Nothing is hand-picked, so adding a paper to _data/publications.yml
  with a date is all it takes to surface it here.
{%- endcomment -%}
{% assign dated = site.data.publications | where_exp: "p", "p.date" | sort: "date" | reverse %}
{% assign recent = dated | slice: 0, 6 %}
{% include pub-compact.html entries=recent %}

[All publications and talks →](/publications/)
{: .more}

## Education

- **Ph.D., Mechanical Engineering** — Carnegie Mellon University, expected May 2027. Advised by Christopher McComb and Noelia Grande Gutiérrez.
- **M.S., Mechanical Engineering** — Carnegie Mellon University, August 2024. Earned en route to the Ph.D.
- **B.Eng., Mechanical Engineering & B.A., German** — Shanghai Jiao Tong University, June 2022. Dual-degree program.
{: .edu}
