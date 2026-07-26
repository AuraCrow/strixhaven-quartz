---
aliases:
 - 
---

> [!infobox| left no-th only-icon corners]
> # <font color="#ffffff">Biblioplexia</font>
> ![[Biblioplexia-img.png| cover]]
> # <font color="#ffffff">Info</font>
> |  |  |
> | ---- | ---- |
> | **Tipo de lugar** | Biblioteca |
> | **Zona** | Campus Central |
> | **Otros** |  |
> 
> > [!footer]
> > </br>

##### Descripción

El centro de Strixhaven es el Biblioplexia, la biblioteca principal de la universidad. En el corazón de la biblioteca se encuentra una maraña, un enredo en el tejido de la magia, que brilla como un sol en miniatura en el gran Salón de los Oráculos. Un arco estelar llamado el Arco del Alba se curva en el cielo sobre la biblioteca, marcando su ubicación como un centro de aprendizaje místico.

Arcos dan la bienvenida a las mentes inquisitivas en la biblioteca. En su interior, casi todas las superficies, desde el suelo hasta el alto techo, están repletas de montones de libros. El interior del Biblioplexia es vasto, con largos pasillos, cámaras de archivo lo bastante altas como para tener su propio clima, e incluso estanques y pasajes a modo de foso que solo pueden cruzarse en barca.

Cinco líneas de torres-faro irradian desde el Biblioplex como enormes radios. Estas Antorchas del Conocimiento se extienden hasta los cinco campus de las facultades y más allá, adentrándose más de cien millas en el campo circundante. Arden perpetuamente con una llama mágica, simbolizando el camino hacia el saber y la huida de la ignorancia.

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

#Lugares #CampusCentral 