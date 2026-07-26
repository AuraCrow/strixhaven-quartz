---
cssclasses:
 - banner
 - banner-gradient
aliases:
  - 
---
![[prismari-logo-2.png]]

</br>

> [!infobox| left no-th only-icon corners]
> # <font color="#ffffff">Campus de Prismari</font>
> ![[Prismari-campus.png| cover]]
> # <font color="#ffffff">Info</font>
> |  |  |
> | ---- | ---- |
> | **Tipo de lugar** | Campus |
> | **Zona** | Strixhaven |
> | **Otros** |  |
> 
>  ##### Sitios de interes
>  -----
> - [[Camino Opus]]
> - [[Salón de Conjurot]]
> - [[Vientofuria]]
> 
> > [!footer]
> > </br>

##### Descripción

Al suroeste del campus central, el campus de Prismari se encuentra en una región de rocas dentadas, escarpados pináculos y una intensa actividad geotérmica.

<div style="clear: both;"></div>

###### Apariciones en el Journal
```dataviewjs
// Notas de sesión dentro de la carpeta "La Gaceta"
const pages = dv.pages('"La Gaceta"')
  .where(p => p.file.name.startsWith("La Gaceta Nº. "));

const currentPage = dv.current();
let aliases = currentPage.file.aliases ?? currentPage.file.frontmatter?.aliases ?? [];
const currentName = currentPage.file.name;
const names = [...aliases, currentName].filter(Boolean);


const pagesWithContent = await Promise.all(
  pages.map(async page => {
    const content = await dv.io.load(page.file.path);
    return { page, content };
  })
);

let rows = [];

for (const { page, content } of pagesWithContent) {
  const sentences = content.split(/(?<=[.!?])\s+/);

  let snippets = [];

for (let i = 0; i < sentences.length; i++) {
  const s = sentences[i];

  const mentioned = names.some(name => 
    s.includes(`[[${name}]]`) || s.includes(`[[${name}|`)
  );

  if (mentioned) {
    const next = sentences[i + 1] ?? "";
    const snippet = (s + " " + next).trim();
    snippets.push(snippet);
  }
}

  if (snippets.length > 0) {
    // Todas las menciones de esta sesión, separadas por párrafo
    rows.push([
      dv.fileLink(page.file.path),
      snippets.join("\n\n")
    ]);
  }
}

dv.table(["Gaceta", "Texto"], rows);
```

#Lugares