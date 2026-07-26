---
aliases:
 - El rincón del arco
 - la taberna
---

> [!infobox| left no-th only-icon corners]
> # <font color="#ffffff">El Rincón del Arco</font>
> ![[Lugar_filler.png| cover]]
> # <font color="#ffffff">Info</font>
> |  |  |
> | ---- | ---- |
> | **Tipo de lugar** | Taberna |
> | **Zona** | Campus Central |
> | **Otros** |  |
> 
> 
> > [!footer]
> > </br>

##### Descripción

En el extremo occidental del Arco del Alba, donde este se encuentra con el suelo, se alza otro hito más pequeño de la universidad: la Taberna del Arco, que sirve como punto de encuentro para los estudiantes más veteranos. La mayoría de los clientes acuden por la música en vivo, la deliciosa comida grasienta y las diversas pociones y bebidas. Otros vienen a resolver sus diferencias en salvajes duelos en el terreno detrás de la taberna. El encargado de la taberna es un orco amable pero estricto llamado Tulk «el Corpulento» Colmillo de Marfil.

###### Lore

> [!pinned|medium]+ NPCs
> </br>



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