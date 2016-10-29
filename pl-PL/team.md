---
layout: default
title: Nasz zespół &middot; Język programowania Rust

localized-teams:
  Core team:
    name: Zespół główny
    responsibility: "ogólny kierunek projektu, przewodzenie podgrupom, kwestie przekrojowe"
  Language design team:
    name: Zespół projektujący język
    responsibility: "projektowanie nowych funkcji języka"
  Library team:
    name: Zespół bibliotek
    responsibility: "standardowa biblioteka Rusta, crate'y rust-lang, konwencje"
  Compiler team:
    name: Zespół kompilatora
    responsibility: "wnętrze kompilatora, optymalizacje"
  Tooling and infrastructure:
    name: Narzędzia i infrastruktura
    responsibility: "wsparcie narzędzi (np. Cargo, rustup), infrastruktura ciągłej integracji"
  Community team:
    name: Zespół społeczności
    responsibility: "koordynacja wydarzeń, użytkownicy komercyjni, materiały dydaktyczne, ekspozycja i popularyzacja języka"
  Documentation team:
    name: Zespół dokumentacji
    responsibility: "zapewnianie Rustowi fantastycznej dokumentacji"
  Moderation team:
    name: Zespół moderacji
    responsibility: "pomoc w utrzymaniu <a href='https://www.rust-lang.org/conduct.html'>kodeksu postępowania</a>"
  Style team:
    name: Zespół stylu
    responsibility: "tymczasowy \"zespół uderzeniowy\", zajmujący się decydowaniem o wytycznych dotyczących stylu i konfiguracją Rustfmt (proces opisany w <a href='https://github.com/rust-lang/rfcs/blob/master/text/1607-style-rfcs.md'>RFC 1607</a>)"
  Rust team alumni:
    name: W stanie spoczynku
    responsibility: "cieszenie się zasłużoną emeryturą"
---

<style type="text/css">
.headshot {
  border: 1px solid #888;
  width: 140px;
}

.person {
  display: inline-block;
  position: relative;
  margin-bottom: 20px;
}
.lead { font-weight: bold; }
.lead .name::after { content: " (lead)"; }
.details {
  display: none;
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: rgba(0, 0, 0, 0.5);
  color: white;
  font-weight: normal;
}
.person:hover .details {
   display: block;
}

.headshots {
  text-align: center;
  margin: 0px auto;
  padding: 0;
  width: 700px;
  max-width: 100%;
  list-style: none;
}
</style>

# The Rust Team

Projekt Rust jest
[zarządzany](https://github.com/rust-lang/rfcs/blob/master/text/1068-rust-governance.md)
przez wiele zespołów, z których każdy jest poświęcony specyficznemu zadaniu. Poniżej
znajdują się poszczególne składy, w porządku alfabetycznym.

Aby skontaktować się z zespołem, zamieść swoje pytanie lub komentarz na [the Internals
forum](https://internals.rust-lang.org/) i otaguj swój post kategorią odpowiadającą
nazwie zespołu. Zauważ, że zgłoszenia dotyczące bezpieczeństwa powinny być zgodne z
[procedurą ujawniania problemów dotyczących bezpieczeństwa](security.html).

{% for team in site.data.team.teams %}
<section id="{{ team.name | replace:' ','-' }}">
<h2> {{ page.localized-teams[team.name].name | default: team.name }} </h2>

<strong>Obowiązki</strong>: <em>{{ page.localized-teams[team.name].responsibility | default: team.responsibility }}</em>

<br />

{% if team.email %}
  <strong>Contact</strong>:
  <a href="mailto:{{ team.email | uri_escape }}">{{ team.email }}</a>
{% endif %}

<ul class="headshots">
{% for nick in team.members %}
  {% assign person = site.data.team.people[nick] %}
  {% if person.site %}
    {% assign sitename = person.site %}
  {% else %}
    {% assign sitename = "github" %}
  {% endif %}
  {% assign website = site.data.team.sites[sitename] %}
  <li class="person {% if team.lead and team.lead == nick %}lead{% endif %}">
  <a href="{{ website.url | replace:'%nick',nick }}">
    <div class="name">{{ person.name }}</div>
    <div class="details">
      <div>irc: {% if person.irc %}{{ person.irc }}{% else %}{{ nick }}{% endif %}</div>
      {% if person.ex-teams %}
      <div>teams: {% for ex-team in person.ex-teams %}{% if forloop.first == false %}, {% endif %}{{ page.localized-ex-teams[ex-team] | default: ex-team }}{% endfor %}</div>
      {% endif %}
    </div>
    <img class="headshot" src="{{ website.avatar | replace:'%nick',nick }}" alt="{{ person.name }}">
  </a>
</li>
{% endfor %}
</ul>
</section>
{% endfor %}
