---
title: "Mallar för inlägg"
excerpt: "Alla presentationsval temat erbjuder för ett inlägg — med YAML att kopiera."
categories:
  - verkstaden
  - artiklar
tags:
  - mallar
  - referens
locale: sv-SE
toc: true
toc_label: "Innehåll"
toc_icon: "list"
toc_sticky: true
header:
  overlay_image: /assets/images/demo-overlay.svg
  overlay_filter: 0.5
  show_overlay_excerpt: true
  caption: "Platshållarbild"
  teaser: /assets/images/demo-teaser.svg
gallery:
  - url: /assets/images/demo-gallery-1.svg
    image_path: /assets/images/demo-gallery-1.svg
    alt: "Platshållare ett"
    title: "Visas vid hovring och i ljusbordet"
  - url: /assets/images/demo-gallery-2.svg
    image_path: /assets/images/demo-gallery-2.svg
    alt: "Platshållare två"
  - url: /assets/images/demo-gallery-3.svg
    image_path: /assets/images/demo-gallery-3.svg
    alt: "Platshållare tre"
feature_row:
  - image_path: /assets/images/demo-gallery-1.svg
    alt: "Platshållare ett"
    title: "Tre i bredd"
    excerpt: "`feature_row` ger jämnt fördelade kort."
  - image_path: /assets/images/demo-gallery-2.svg
    alt: "Platshållare två"
    title: "Med knapp"
    excerpt: "Varje kort kan ha en länk och en knapptext."
    url: "/verkstaden/"
    btn_label: "Öppna"
    btn_class: "btn--primary"
  - image_path: /assets/images/demo-gallery-3.svg
    alt: "Platshållare tre"
    title: "Bara bild"
    excerpt: "Utelämna titeln för ett enklare kort."
---

Det här är en referens över allt du kan styra i ett inläggs *front matter*.
Kopiera YAML-blocket från det avsnitt du behöver.

**Läs så här.** Vissa val syns direkt i den här artikeln — den har overlay-rubrik,
innehållsförteckning, galleri, kortrad och notiser. Övriga går inte att visa här,
eftersom ett inlägg bara kan ha *en* layout och *en* rubrik. De redovisas som kod.
{: .notice--info}

## Grundinställningar

Utan något extra i front matter får ett inlägg det som är satt som standard i
`_config.yml`: författarkort i sidofältet, lästid, delningsknappar och relaterade
inlägg.

```yaml
---
title: "Rubrik"
excerpt: "Visas under rubriken och i listningar."
categories:
  - verkstad
  - artiklar
tags:
  - etikett
---
```

Kategorierna styr adressen, eftersom sajten använder `permalink: /:categories/:title/`.
`[verkstad, artiklar]` ger `/verkstad/artiklar/rubriken/`.

Stäng av delarna du inte vill ha, var för sig:

```yaml
author_profile: false
read_time: false
share: false
related: false
comments: false
```

## Rubriker

### Rubrikbild

En bild ovanför rubriken. Den lägger sig *inte* över texten.

```yaml
header:
  image: /assets/images/demo-header.svg
  image_description: "Alt-text för skärmläsare."
  caption: "Bildtext med **markdown** och [länkar](https://jekyllrb.com)."
```

Sätt alltid `image_description` — det blir bildens `alt`. Utan den läses bilden
upp som omärkt.
{: .notice--warning}

### Overlay-rubrik

Den här artikeln använder den. Rubrik och utdrag ligger *ovanpå* bilden, och
`overlay_filter` mörkar bilden så texten går att läsa.

```yaml
header:
  overlay_image: /assets/images/demo-overlay.svg
  overlay_filter: 0.5              # 0–1, eller rgba(...)
  show_overlay_excerpt: true       # false döljer utdraget
  caption: "Bildtext"
  actions:
    - label: "Primär knapp"
      url: "/verkstaden/"
```

`overlay_filter` tar även en färg, vilket är bra när en rak svart slöja blir platt:

```yaml
overlay_filter: rgba(45, 59, 66, 0.6)
```

Flera `actions` blir en rad med knappar.

### Enfärgad rubrik

Samma effekt utan bild — billigast möjliga, ingen extra nedladdning:

```yaml
header:
  overlay_color: "#2c5f7c"
  show_overlay_excerpt: true
```

### Videorubrik

```yaml
header:
  video:
    id: "-Fydq8YSPS0"      # enbart id:t, inte hela adressen
    provider: "youtube"    # eller vimeo
```

Två saker att känna till: sidan gör ett anrop till en tredjepart när den visas
(temat bäddar in via `youtube-nocookie.com`, så inga spårningskakor sätts förrän
någon trycker på play), och `id` är just id:t. Klistrar du in en hel
`https://youtube.com/watch?v=…` händer ingenting alls — ingen spelare, inget felmeddelande.
{: .notice--warning}

## Innehållsförteckning

Byggs automatiskt av rubrikerna. Den här artikeln använder den — se sidofältet.

```yaml
toc: true
toc_label: "Innehåll"    # rubrik ovanför listan
toc_icon: "list"         # valfritt Font Awesome-namn
toc_sticky: true         # följer med vid skrollning
```

Rubrikerna måste vara riktiga markdown-rubriker (`##`). En fetstilad rad räknas inte.

## Layouter

### Bred layout

```yaml
classes: wide
author_profile: false
```

`wide` tar bort marginalen som annars reserverar plats åt sidofältet. Den tar
*inte* bort sidofältet i sig — låter du författarkortet vara kvar krockar det med
den breddade texten. Kombinera därför alltid med `author_profile: false`.
{: .notice--danger}

Bra för breda tabeller, långa kodblock och skärmbilder.

### Splash

```yaml
layout: splash
header:
  overlay_color: "#3f3f5a"
```

`splash` skalar bort allt som hör inlägget till — datum, sidofält, lästid,
delning, relaterade inlägg. Kvar blir rubriken och innehållet i full bredd.
Använd den till landningssidor snarare än artiklar. Sajtens startsida använder den.

## Bildgalleri

Bilderna definieras i front matter, rutnätet placeras med en include:

{% include gallery caption="Tre platshållare. Bildtexten klarar **markdown**." %}

```yaml
gallery:
  - url: /assets/images/demo-gallery-1.svg          # full storlek, för ljusbordet
    image_path: /assets/images/demo-gallery-1.svg   # miniatyr
    alt: "Platshållare ett"
    title: "Text vid hovring"
```

{% raw %}
```liquid
{% include gallery caption="Valfri bildtext med **markdown**." %}
```
{% endraw %}

Antalet kolumner följer antalet bilder — två bilder ger två kolumner, tre ger tre.
Har du flera gallerier i samma inlägg ger du varje ett id:

{% raw %}
```liquid
{% include gallery id="galleri_vanster" class="half" %}
```
{% endraw %}

## Kortrad

{% include feature_row %}

```yaml
feature_row:
  - image_path: /assets/images/demo-gallery-1.svg
    alt: "Platshållare"
    title: "Tre i bredd"
    excerpt: "Korttext."
    url: "/verkstaden/"
    btn_label: "Öppna"
    btn_class: "btn--primary"
```

{% raw %}
```liquid
{% include feature_row %}
```
{% endraw %}

## Notiser

Färgade rutor för varningar, tips och sidoinformation.

**Standard.** Neutral grå ruta för sidoinformation.
{: .notice}

**Primär.** Följer temats accentfärg och ändras alltså med skinnet.
{: .notice--primary}

**Info.** Stödjande detaljer.
{: .notice--info}

**Varning.** Något som ställer till det om du missar det.
{: .notice--warning}

**Klart.** Bekräftelse på att något gick vägen.
{: .notice--success}

**Fara.** Förstörande eller svårt att ångra.
{: .notice--danger}

Syntaxen är en attributrad direkt under stycket:

```markdown
**Varning.** Något som ställer till det.
{: .notice--warning}
```

Attributet fäster bara på ett stycke. Behöver du flera stycken i samma ruta får du
ta HTML, med `markdown="1"` så att markdown fortsätter fungera inuti:

<div class="notice--info" markdown="1">
**En längre notis.**

Med `markdown="1"` funkar kod, länkar och listor som vanligt:

- fortfarande en lista
- fortfarande `kod`
</div>

Tillgängliga: `.notice`, `.notice--primary`, `.notice--info`, `.notice--warning`,
`.notice--success`, `.notice--danger`.

## Eget sidofält

Byt ut författarkortet mot egen text, egen bild eller en meny:

```yaml
author_profile: false
sidebar:
  - title: "Egen rubrik"
    image: /assets/images/demo-sidebar.svg
    image_alt: "Platshållare"
    text: "Titel, bild och text är alla valfria."
  - title: "Ett andra block"
    text: "Sidofältet tar en lista, så block staplas."
```

Sidofältet kan också rendera en meny från `_data/navigation.yml`:

```yaml
sidebar:
  nav: "verkstaden"
```

Det är samma nycklar som sajtens toppmeny använder.

## Länkinlägg

```yaml
link: https://jekyllrb.com/docs/front-matter/
```

Rubriken pekar då på den adressen i stället för på inlägget, och en knapp med
direktlänk hamnar under texten. Inlägget behåller sin egen permalänk och syns
fortfarande i listningar och flöden.

## Puffbild i listningar

```yaml
header:
  teaser: /assets/images/demo-teaser.svg
```

Puffbilden används som miniatyr i listningar — men **bara** när listan renderas
som rutnät. I listläge ignoreras den utan felmeddelande:

{% raw %}
```liquid
{% include archive-single.html post=post type="grid" %}
```
{% endraw %}

## Typografi

Så här ser vanlig markdown ut i temat — bra att stämma av mot när innehåll flyttas in.

### Text

Vanlig text med **fet stil**, *kursiv*, `kod`, [länk](https://jekyllrb.com),
~~genomstruken~~ och en fotnot.[^1]

[^1]: Fotnoter samlas längst ner i inlägget.

### Listor

- Punktlista
- Med en nivå under
  - Underpunkt
  - Ytterligare en
- Tillbaka på översta nivån

1. Numrerad
2. Andra
3. Tredje

### Citat

> Ett blockcitat, för längre citat ur en källa.
>
> <cite>Källhänvisning i ett cite-element</cite>

### Kod

```ruby
def kategorier_for(post)
  post.data["categories"].map(&:downcase)
end
```

```bash
bundle exec jekyll serve --livereload
```

### Tabeller

| Nyckel | Typ | Kommentar |
|---|---|---|
| `title` | sträng | Inläggets rubrik |
| `categories` | lista | Styr adressen via permalänkmönstret |
| `tags` | lista | Fritt valda |

## Snabbreferens

| Vill du ha | Front matter |
|---|---|
| Bild ovanför rubriken | `header.image` |
| Rubrik ovanpå bild | `header.overlay_image` + `overlay_filter` |
| Enfärgad rubrik | `header.overlay_color` |
| Video som rubrik | `header.video.id` + `provider` |
| Innehållsförteckning | `toc: true`, `toc_sticky: true` |
| Full bredd, inget sidofält | `classes: wide` + `author_profile: false` |
| Landningssida utan ramverk | `layout: splash` |
| Bildrutnät | `gallery:` + `{% raw %}{% include gallery %}{% endraw %}` |
| Kort i rad | `feature_row:` + `{% raw %}{% include feature_row %}{% endraw %}` |
| Eget sidofält | `author_profile: false` + `sidebar:` |
| Meny i sidofältet | `sidebar.nav: "verkstaden"` |
| Rubrik som länkar bort | `link:` |
| Miniatyr i listning | `header.teaser` (kräver `type="grid"`) |
