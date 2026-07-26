---
cssclasses:
 - banner
 - banner-gradient
aliases:
  - 
---
![[witherbloom-logo-2.png]]

> [!infobox| corners no-th only-icon]
> 
> # Witherbloom
> 
> ![[witherbloom-logo.png| cover]]
> 
> # Info
> 
> |  |  |
> | ---- | ---- |
> | **Tipo** | Escuela |
> | **Líder/es** |[[Lisette]] </br>[[Valentin]]|
> </br>
> 
> > [!footer]
> > </br>

</br>

##### Lore

En Witherbloom, la Facultad de Estudios de la Esencia, los magos extraen poder de las fuerzas opuestas de la vida y la muerte. Estos magos elaboran sus hechizos a partir de componentes naturales y la esencia de criaturas vivas, usando ese poder para curar o dañar a los vivos o para resucitar y suplicar a los muertos. Pueden hacer que bosques enteros florezcan de la nada o invocar viejas maldiciones que azotan la carne de los huesos. Algunos magos de Witherbloom defienden los ecosistemas de la contaminación, mientras que otros se deleitan con el poder de la corrupción. Suelen estar en casa montando cocodrilos zombis por un río lánguido, recogiendo hierbas para crear pociones para tratar enfermedades, meditando sobre un coro de ranas del pantano o invocando temibles avatares de la naturaleza.
</br>

##### Estudios y filosofía

El plan de estudios de la facultad de Witherbloom se centra en varias ciencias, que giran en torno a las ciencias de la vida. La biología, la ecología, la botánica, la química y las ciencias afines se combinan con el estudio y la manipulación de la energía mágica del Plano Positivo y el Plano Negativo, las fuerzas primordiales de la vida y la muerte. El plan de estudios de Witherbloom comparte cierta superposición con el análisis de Quándrix de los patrones matemáticos en la naturaleza.


## Crecimiento y Decadencia

Los dos decanos de Witherbloom se llaman tradicionalmente el Decano de la Raíz y el Decano de la Vena. Estos títulos son una forma un tanto abstracta de enmarcar la división central de la filosofía de la universidad: ¿es el crecimiento o la decadencia la fuerza impulsora de la naturaleza? La filosofía de la raíz (crecimiento) se centra en la vida y su incontenible impulso para prosperar. Esta vista celebra la diversidad y adaptabilidad de las formas de vida, desde las células más pequeñas hasta las redes más complejas de seres vivos. La filosofía del crecimiento afirma que el impulso de sobrevivir y reproducirse es el principio más esencial del cosmos. Los magos que adoptan este punto de vista ejercen energía positiva y practican la magia curativa. La filosofía de la vena (descomposición) se centra en la inevitabilidad de la muerte y la descomposición. Su nombre tradicional proviene de la prominencia de los vampiros dentro de la universidad, cuyas concepciones de drenar la vida a través de la vena han demostrado durante mucho tiempo un importante contrapeso a la filosofía de crecimiento de Witherbloom. La filosofía de la decadencia ve la energía vital como un recurso para ser consumido, en lugar de un bien para ser alimentado por sí mismo. Los magos que adoptan este punto de vista ejercen energía negativa y practican la nigromancia.
</br> 

> [!pinned|large]+ Decanos y Profesores
> >[!article]
> > [[Lisette]]
> > Decana de la Raíz
> >
> > [[Valentin]]
> > Decano de la Vena
> > 
> > <span class="column-break"></span>
> >
> > [[Sauceocaso, Vidente de la Esencia]]
> > 	Profesora del Crecimiento
> >
> > [[Verelda Lang, Arcano-Bióloga]]
> > Profesora del Crecimiento
> >
> > [[Tívash, Invocador sombrío]]
> > Profesor de la Decadencia

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