---
cssclasses:
 - banner
 - banner-gradient
aliases:
  - 
---
![[lorehold-logo-2.png]]

> [!infobox| corners no-th only-icon]
> 
> # Lorehold
> 
> ![[lorehold-logo.png| cover]]
> 
> # Info
> 
> |  |  |
> | ---- | ---- |
> | **Tipo** | Escuela |
> | **Líder/es** |[[Augusta Tullus]] </br>[[Plargg]]|
> </br>
> 
> > [!footer]
> > </br>

</br>

##### Lore

Lorehold es el Colegio de Arqueomancia, un término que describe la exploración de objetos arcanos a través de la magia. Sus magos exploran el pasado estudiando sobre sitios arqueológicos, invocando energía mágica de tomos antiguos y convocando a los espíritus de personajes históricos muertos hace mucho tiempo. Los magos de Lorehold viajan a lo largo y ancho del mundo, reuniendo reliquias de edades pasadas y aprendiendo lenguas muertas para desempaquetar los secretos de la historia.
</br>

##### Estudios y filosofía

La facultad de Lorehold se dedica al estudio de la historia, entendida ampliamente como la que incluye los diversos aspectos de la cultura, el comportamiento y las relaciones sociales que dan forma a los acontecimientos históricos. Sus estudios incluyen varias subdivisiones de la historia (historia militar, historia social, historia cultural), arqueología, antropología, psicología, sociología, religión y economía. Se superpone con Prismari en el campo de la historia del arte, con algunos estudiantes dividiendo sus estudios entre las dos facultades. Los magos de Lorehold usan su magia para desenterrar secretos y compartir la iluminación.


## Orden y Caos

Los dos decanos de Lorehold llevan los títulos Decano del Orden y Decano del Caos, ya que el orden contra el caos resume el conflicto fundamental en el corazón de la filosofía de Lorehold. Este conflicto gira en torno a las fuerzas que subyacen e impulsan la historia. ¿El curso del tiempo conduce hacia un estado ideal bien ordenado o se está convirtiendo lentamente en un caos? ¿Hay patrones profundos ocultos en los textos históricos, o es el tiempo una serie de coincidencias y casualidades? La perspectiva del orden enfatiza las estructuras que unen a las personas (ley, religión, economía, educación, clase social, etc.) y cómo esas estructuras impulsan los acontecimientos históricos. El orden se centra en los cambios sistémicos y las acciones colectivas de las personas. La perspectiva del caos, por el contrario, enfatiza las acciones individuales, los lazos personales de familiares y amigos, y la fuerza disruptiva de las personas solitarias y apasionadas en la historia. Los estudiosos del caos gravitan hacia el descubrimiento imprudente y el espíritu de aventura en su investigación del pasado: la esencia y la emoción de la historia sobre la precisión o el procedimiento.
</br>

> [!pinned|large]+ Decanos y Profesores
> >[!article]
> > [[Augusta Tullus]]
> > Decana del Orden
> >
> > [[Plargg]]
> > Decano del Caos
> > 
> > <span class="column-break"></span>
> >
> > [[Hofri Forjafantasmas]]
> > Profesor del Orden
> >
> > [[Osgir, el Reconstructor]]
> > Profesor del Orden
> >
> > [[Losheel, erudita mecánica]]
> > Profesora del Caos

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