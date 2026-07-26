---
cssclasses:
 - banner
 - banner-gradient
aliases:
  - 
---
![[silverquill-logo-2.png]]

> [!infobox| corners no-th only-icon]
> 
> # Silverquill
> 
> ![[silverquill-logo.png| cover]]
> 
> # Info
> 
> |  |  |
> | ---- | ---- |
> | **Tipo** | Escuela |
> | **Líder/es** |[[Shaile Talonrook]] </br> [[Embrose Lu]]|
> </br>
> 
> > [!footer]
> > </br>

</br>

##### Lore

Silverquill es el Colegio de la Elocuencia, y sus magos, elegantes, intimidantes y motivados, son maestros de la magia de las palabras. Crean hechizos a partir de la poesía de batalla hablada o manifestaciones mágicas de la palabra escrita, dibujando patrones de tinta rúnica en el aire. Estos magos son líderes naturales, ferozmente competitivos, con un ingenio penetrante y una actitud de nunca quedar en segundo lugar.
</br>

##### Estudios y filosofía

El plan de estudios de Silverquill gira en torno a las palabras, y abarca la literatura (que incluye ficción, ensayos, teatro y poesía), idiomas, lingüística, oratoria, retórica y representación dramática. Los estudiantes de otras universidades a menudo toman cursos de Silverquill para mejorar sus habilidades de comunicación, aprendiendo a hablar y escribir de manera más efectiva sobre su campo de estudio principal. Silverquill y Prismari ven una superposición en el área de las artes escénicas, con Silverquill enfatizando la interpretación verbal y Prismari enfocándose más en la danza y otras formas de movimiento.


## Resplandor y Sombra

Los dos decanos de Silverquill se llaman el Decano del Resplandor y el Decano de la Sombra, destacando el uso de la metáfora por parte de la universidad para describir sus diferencias filosóficas. La metáfora del resplandor y la sombra toma forma concreta en la magia de Silverquill a medida que los estudiantes aprenden a manifestar una luz brillante o una oscuridad total con sus hechizos. El argumento fundamental entre los estudiosos de Silverquill se centra en el propósito de la comunicación. ¿Es para ayudar a otros o promover una agenda personal? ¿La literatura mejora desinteresadamente a la sociedad o promueve egoístamente los propios objetivos? La perspectiva de Resplandor visualiza el lenguaje como la luz del sol que emana del hablante o escritor para iluminar a otros y hacer del mundo un lugar más brillante. Los magos que adoptan este punto de vista usan sus habilidades lingüísticas y su magia para animar y empoderar a otros, para arrojar luz sobre los males de la sociedad e inspirar lo mejor en quienes los rodean. La perspectiva de la sombra se centra en el poder del lenguaje para apuñalar, exponer verdades punzantes y ofuscar secretos. La magia de los magos sombríos a menudo se manifiesta como rayos u hojas de oscuridad o manchas de tinta que fluye, y sus efectos van desde un aguijón de vergüenza hasta un asalto a la energía vital del objetivo.
</br>

> [!pinned|large]+ Decanos y Profesores
> >[!article]
> > [[Shaile Talonrook]]
> > Decana del Resplandor
> >
> > [[Embrose Lu]]
> > Decano de las Sombras
> > 
> > <span class="column-break"></span>
> >
> > [[Breena, la Demagoga]]
> > Profesora de las Sombras
> >
> > [[Brenneth Blackstone, Estrella de la Escritura]]
> > Profesor de las Sombras
> >
> > [[Nils, Ejecutor de la Disciplina]]
> > Profesor del Resplandor

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