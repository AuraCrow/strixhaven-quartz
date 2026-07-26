---
cssclasses:
 - banner
 - banner-gradient
aliases:
  - 
---
![[silverquill-logo-2.png]]

</br>

> [!infobox| left no-th only-icon corners]
> # <font color="#ffffff">Escenario de la Rosa</font>
> ![[Lugar_filler.png| cover]]
> # <font color="#ffffff">Info</font>
> |  |  |
> | ---- | ---- |
> | **Tipo de lugar** | Anfiteatro |
> | **Zona** | Campus de Silverquill |
> 
> > [!footer]
> > </br>

##### Descripción

El escenario de la rosa es una plataforma circular giratoria en el campus de Silverquill. Tiene un fondo de rosas hechas de tinta mágica (tributos dejados por los espectadores de pasadas funciones), lo que crea una excelente acústica. Los estudiantes de magia se reúnen en el escenario de la rosa para practicar actuaciones, entrenar o participar en duelos de honor. Los miembros de la facultad a menudo observan actuaciones en el escenario de la rosa, entrenando a los estudiantes en sus exhibiciones mágicas y retóricas.

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