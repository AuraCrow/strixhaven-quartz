---
cssclasses:
 - banner
 - banner-gradient
aliases:
  - 
---
![[prismari-logo-2.png]]

> [!infobox| corners no-th only-icon]
> 
> # Prismari
> 
> ![[prismari-logo.png| cover]]
> 
> # Info
> 
> |  |  |
> | ---- | ---- |
> | **Tipo** | Escuela |
> | **Líder/es** |[[Uvilda Mistcoiler]] </br>[[Nassari]]|
> </br>
> 
> > [!footer]
> > </br>

</br>

##### Lore

Prismari, la Facultad de Artes Elementales, se dedica al estudio y la práctica del arte entrelazado con la magia. Los estudiantes de magia de Prismari ejercen la magia en espectáculos de creatividad: obras maestras de magia llamativa y exagerada. Usan magia elemental para expresar quiénes son y cómo ven el mundo, a menudo combinando diferentes tipos de energía (fuego, agua, aire, tierra, relámpagos, calor, frío) en poderosas expresiones de conflicto y armonía.
</br>

##### Estudios y filosofía

La facultad está dedicada a las artes. Sus eruditos ven el arte como la forma fundamental de autoexpresión y la magia como una herramienta, un medio y una inspiración. Los estudios de Prismari se centran en las artes visuales (incluidas la arquitectura, la pintura y la escultura) y las artes escénicas (como la danza, la música y el teatro). El plan de estudios se superpone con Lorehold en el campo de la historia del arte y con Silverquill en las artes literarias, y algunos estudiantes dividen su tiempo entre Prismari y una de esas otras escuelas para seguir estos campos interdisciplinarios. Los magos Prismari usan magia para tejer los elementos en sus creaciones; pueden unir fuego junto con pintura, cerámica o tela, o pueden coreografiar obras elaboradas que unen los movimientos de un bailarín con ráfagas y remolinos de aire.


## Prefección y Expresión

Los dos decanos de Prismari llevan los títulos de Decano de la perfección y Decano de la expresión, y a menudo expresan el conflicto fundamental de su filosofía como perfección frente a expresión o, a veces, intelecto frente a emoción. ¿Cuál es el propósito del arte? ¿Es para hacer que la gente piense cosas o para hacer que la gente sienta cosas? ¿Se supone que debe ser cuidadosamente pensado o crudo y espontáneo? ¿El dominio del arte es una cuestión de perfeccionar técnicas precisas hasta un punto de perfección o de expresar perfectamente un estado emocional crudo? ¿El arte aspira a expresar verdades universales o intensamente personales?
</br>

> [!pinned|large]+ Decanos y Profesores
> >[!article]
> > [[Uvilda Mistcoiler]]
> > - Decana de la Perfección
> >
> > [[Nassari]]
> > - Decana de la Expresión
> > 
> > <span class="column-break"></span>
> >
> > [[Veyran, Voz de la Dualidad]]
>  > - Profesor de la Perfección
> > 
> > [[Zaffai, Director de Truenos]]
> > - Profesor de la Expresión
> > 
> > [[Arkin Minexes, Instructor Alegre]]
> > - Profesor de la Expresión

</br>



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

#Facciones #Escuelas