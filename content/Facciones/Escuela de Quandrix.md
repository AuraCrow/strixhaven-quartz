---
cssclasses:
 - banner
 - banner-gradient
aliases:
  - 
---
![[quandrix-logo-2.png]]

> [!infobox| corners no-th only-icon]
> 
> # Quandrix
> 
> ![[quandrix-logo.png| cover]]
> 
> # Info
> 
> |  |  |
> | ---- | ---- |
> | **Tipo** | Escuela |
> | **Líder/es** |[[Kianne]] </br>[[Imbraham]]|
> </br>
> 
> > [!footer]
> > </br>

</br>

##### Lore

Quándrix es el Colegio de la Numeromancia, un término que abarca el estudio de patrones, fractales y simetrías para ejercer poder sobre las matemáticas fundamentales de la naturaleza. Los magos de Quándrix pueden invocar criaturas hechas de fractales o convertir teorías abstractas en imponentes patrones en espiral. Les encanta expandirse y multiplicarse; pueden aumentar su conocimiento o tamaño doblando números. Saben combinar lo teórico y lo natural, desde la tela de sus túnicas hasta la naturaleza de sus hechizos, hacen uso de elementos repetidos, simetrías inteligentes y geometría sorprendente para expresar las complejas verdades que estudian.
</br>

##### Estudios y filosofía

Los estudios realizados dentro de la facultad de Quándrix incluyen matemáticas, física, lógica, estadística, metafísica y varios campos de la magia teórica. Los estudiantes de otras universidades ocasionalmente profundizan en los cursos de Quándrix para reforzar los fundamentos teóricos de sus estudios, y los estudios de naturaleza de Quándrix y las exploraciones de biología práctica de Flosmarcitus tienen una superposición significativa.


## Sustancia y teoría

Los dos decanos de Quándrix llevan los títulos de Decano de Sustancia y Decano de Teoría, lo que refleja la división filosófica dentro de la facultad. ¿Son las matemáticas una fuerza natural que existe en el universo independiente de las construcciones de mentes inteligentes, o es un marco teórico creado por quienes las estudian? ¿Es el trabajo del erudito descubrir lo que es o definir lo que podría ser? La perspectiva de la sustancia enfatiza la realidad física. Desde este punto de vista, las matemáticas están encarnadas en las fuerzas naturales del multiverso, esperando ser descubiertas por aquellos con la fortaleza intelectual para profundizar en esos secretos. Los magos de Quándrix que adoptan este punto de vista usan la magia para dar vida a los conceptos numéricos, creando o alterando la realidad física a partir de la posibilidad matemática. La perspectiva de la teoría se centra en los reinos abstractos de la conjetura y la posibilidad. Sus estudiosos ven las matemáticas como una lente a través de la cual una mente puede comprender el cosmos, no como algo que existe de forma independiente en el mundo. Los magos que adoptan esta perspectiva usan sus hechizos para tejer ilusiones y manipular el tejido de la magia misma.
</br>

> [!pinned|large]+ Decanos y Profesores
> >[!article]
> > [[Kianne]]
> > - Decana de la Sustancia
> >
> > [[Imbraham]]
> > - Decano de la Teoría
> > <span class="column-break"></span>
> >
> > [[Ádrix y Nev, conjuradores gemelos]]
> > - Ándrix, profesor de la Sustancia
> > - Nev, profesor de la Teoría
> >
> > [[Deekah, teórica del fractal]]
> > - Profesora de la Teoría
> > 
> > [[Ruxa, Profesor Paciente]]
> > - Profesor de la Sustancia

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