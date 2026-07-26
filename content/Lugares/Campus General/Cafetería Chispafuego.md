---
aliases:
 - la cafetería
 - Chispafuego
---

> [!infobox| left no-th only-icon corners]
> # <font color="#ffffff">Cafetería Chispafuego</font>
> ![[Lugar_filler.png| cover]]
> # <font color="#ffffff">Info</font>
> |  |  |
> | ---- | ---- |
> | **Tipo de lugar** | Cafetería |
> | **Zona** | Campus Central |
> | **Otros** |  |
> 
> 
> > [!footer]
> > </br>

##### Descripción

En el borde de la plaza del Arco y justo a las afueras del Biblioplexia se alza el acogedor Café Chispafuego, donde los estudiantes se atiborran tanto de información como de cafeína antes de los exámenes. El nombre del café proviene de su bebida característica que el encargado prepara utilizando su magia de fuego. El Chispafuego tiene fama de ser un punto de encuentro para estudiantes de primer año, pero alumnos más veteranos de las cinco facultades pueden verse en su interior a cualquier hora.

###### Lore

> [!pinned|medium]+ NPCs
> Nombre
> > Regente del sitio


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