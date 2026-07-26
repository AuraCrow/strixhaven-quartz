---
cssclasses:
 - banner
 - banner-gradient
aliases:
  - 
---
![[lorehold-logo-2.png]]

</br>

> [!infobox| left no-th only-icon corners]
> # <font color="#ffffff">Pillardrop</font>
> ![[Lugar_filler.png| cover]]
> # <font color="#ffffff">Info</font>
> |  |  |
> | ---- | ---- |
> | **Tipo de lugar** | Ruinas |
> | **Zona** | Campus de Lorehold |
> 
> > [!footer]
> > </br>

##### Descripción

En un abismo natural se ha formado una excavación arqueológica una nueva construcción, Pillardrop es una serie de edificios excavados en acantilados en el campus de Lorehold. Las ruinas y los pasillos mejorados juntos ahora se usan para investigación, trabajo en clase y vivienda. Puentes precarios unen un barrio de Pillardrop con otro, a menudo pasando directamente por los enormes rostros de piedra de estatuas antiguas. Cada clase de Lorehold tiene la historia de un estudiante descuidado que da un paso en falso en uno de estos puentes o en alguna sección particularmente desmoronada de las ruinas, a veces con consecuencias desastrosas, y a veces encuentra la liberación cuando una estatua espiritual aparece de la nada para atrapar al desafortunado estudiante antes de que sufran graves perjuicios.


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