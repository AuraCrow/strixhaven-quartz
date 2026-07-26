---
aliases:
 - plaza central
 - el parque
 - parque central
---

> [!infobox| left no-th only-icon corners]
> # <font color="#ffffff">Plaza del Arco</font>
> ![[plaza-arco.png| cover]]
> # <font color="#ffffff">Info</font>
> |  |  |
> | ---- | ---- |
> | **Tipo de lugar** | Plaza |
> | **Zona** | Campus Central |
> | **Otros** |  |
> 
> > [!footer]
> > </br>

##### Descripción

Justo al sur del Biblioplex, un arco estelar se curva sobre el cielo como un eco más pequeño del Arco del Alba, y un frondoso parque, la plaza del Arco, marca el lugar. Más conocido simplemente como la plaza, el parque es un sitio favorito para los estudiantes —especialmente los de primer año— donde reunirse cuando hace buen tiempo o pasear durante citas.

Algunos de los clubes de la universidad también utilizan el parque para organizar reuniones sociales y juegos, incluyendo partidas de rol en vivo y deportes informales.

###### Lore


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