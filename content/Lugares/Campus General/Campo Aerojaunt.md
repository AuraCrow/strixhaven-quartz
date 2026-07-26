---
cssclasses:
 - banner
 - banner-gradient
aliases:
  - 
---
![[strixhaven-logo-2.png]]

</br>

> [!infobox| left no-th only-icon corners]
> # <font color="#ffffff">Campo Aerojaunt</font>
> ![[Lugar_filler.png| cover]]
> # <font color="#ffffff">Info</font>
> |  |  |
> | ---- | ---- |
> | **Tipo de lugar** | Edificio deportivo |
> | **Zona** | Campus de Strixhaven |
> 
> > [!footer]
> > </br>

##### Descripción

El Campo Aerojaunt fue en su día el principal campo deportivo de la universidad. Ahora, años después de la construcción del Estadio de Strixhaven, el campo se utiliza mucho menos. Su propósito oficial es servir como campo de entrenamiento dedicado para los equipos estudiantiles más destacados de Strixhaven, cuyos partidos oficiales se celebran en instalaciones más modernas en otras zonas del campus.

Sin embargo, los equipos menos competitivos disputan aquí sus encuentros, en particular el Club Intramuros de Silkball. Las rampas elevadas utilizadas en los partidos de silkball fueron construidas de forma permanente en el Campo Aerojaunt, cuyo nombre evoca un popular movimiento de este deporte que consiste en usar la magia para impulsarse y saltar por el aire.

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