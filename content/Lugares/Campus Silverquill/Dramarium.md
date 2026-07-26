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
> # <font color="#ffffff">Dramarium</font>
> ![[Lugar_filler.png| cover]]
> # <font color="#ffffff">Info</font>
> |  |  |
> | ---- | ---- |
> | **Tipo de lugar** | Edificio de práctica |
> | **Zona** | Campus de Silverquill |
> 
> > [!footer]
> > </br>

##### Descripción

El Dramarium es una instalación donde los estudiantes de Silverquill entrenan en fitness, danza, artes marciales y otros actos de rendimiento físico. Los estudiantes pueden aprovechar el espacio de preparación llamado Habitáculo Gris (en realidad, una cadena de habitaciones), que cuenta con salones de peluquería y maquillaje, cabinas de ensayo de voz, espacios de ensayo con espejos e instalaciones de spa. La parte trasera del Dramárium tiene una cámara de privación sensorial especial para estudiantes de magia que quieren un silencio completo en el que meditar.

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