[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/Er6qtz3N)
# Lage-presentasjon-i-Spectacle

Du skal lage en presentasjon fra praksisperioden din. Til dette skal vi bruke react-rammeverket Spectacle

# Hvordan lage en presentasjon med Spectacle

Spectacle er et React-bibliotek for å lage elegante presentasjoner ved hjelp av kode. Her er en guide til hvordan du kommer i gang, fra oppsett til avanserte funksjoner.

## 1. Oppsett og Installering

Først må vi sette opp et nytt prosjekt. Vi bruker **Vite** for å få et raskt og moderne oppsett.

1.  Åpne terminalen din (PowerShell eller lignende).
2.  Naviger til mappen der du vil lagre prosjektene dine.
3.  Kjør følgende kommandoer:

```bash
# Lag en ny mappe for prosjektet (valgfritt hvis du bruker create vite)
mkdir min-presentasjon
cd min-presentasjon

# Opprett et nytt Vite-prosjekt (velg React som rammeverk og JavaScript/TypeScript)
npm create vite@latest .

# Velg:
# > React
# > JavaScript (eller TypeScript hvis du foretrekker det)

# Installer avhengighetene
npm install

# Installer Spectacle
npm install spectacle

# Start utviklingsserveren
npm run dev
```

Nå kan du åpne prosjektet i VS Code (`code .`).

---

## 2. Grunnleggende Struktur

Åpne `src/App.jsx` (eller `.tsx`) og slett alt innholdet. Erstatt det med følgende grunnstruktur for en Spectacle-presentasjon:

```jsx
import React from 'react';
import { Deck, Slide, Heading, Text, FlexBox, DefaultTemplate } from 'spectacle';

function App() {
  return (
    <Deck template={<DefaultTemplate />}>
      
      {/* Slide 1: Tittel */}
      <Slide>
        <FlexBox height="100%" flexDirection="column">
          <Heading>Min Første Presentasjon</Heading>
          <Text>Laget med Spectacle og React</Text>
        </FlexBox>
      </Slide>

      {/* Slide 2: Innhold */}
      <Slide>
        <Heading>Hva er Spectacle?</Heading>
        <Text>
          Spectacle lar deg skrive presentasjoner som React-komponenter.
        </Text>
        <Text>
          Du kan bruke HTML, CSS og JavaScript direkte i slidene dine!
        </Text>
      </Slide>

    </Deck>
  );
}

export default App;
```

### Forklaring av Komponenter

*   **`<Deck>`**: Dette er hovedkomponenten som omslutter hele presentasjonen.
*   **`<Slide>`**: Representerer en enkelt side/lysbilde i presentasjonen.
*   **`<Heading>`**: Brukes for overskrifter (som `<h1>`, `<h2>` osv.).
*   **`<Text>`**: Brukes for vanlig tekst (paragrafer).
*   **`<FlexBox>`**: En hjelpekomponent for layout (basert på CSS Flexbox). Den er veldig nyttig for å midtstille innhold.
    *   `height="100%"`: Sørger for at boksen fyller hele sliden.
    *   `flexDirection="column"`: Legger elementene under hverandre.

---

## 3. Bilder i Presentasjonen

For å legge til bilder, bør du legge bildefilene dine i `public`-mappen eller importere dem direkte hvis de ligger i `src`.

### Metode 1: Importere fra `src` (Anbefalt)
Legg et bilde (f.eks. `katt.jpg`) i `src/assets`-mappen.

```jsx
import React from 'react';
import { Deck, Slide, Heading, Image, FlexBox } from 'spectacle';
// Importer bildet
import bildeAvKatt from './assets/katt.jpg'; 

function App() {
  return (
    <Deck>
      <Slide>
        <FlexBox height="100%" flexDirection="column">
          <Heading>Et bilde av en katt</Heading>
          
          {/* Bruk Image-komponenten */}
          <Image src={bildeAvKatt} width="500px" />
          
        </FlexBox>
      </Slide>
    </Deck>
  );
}
```

### Metode 2: Hente fra nettet
Du kan også bruke en URL direkte i `osrc`-propen.

```jsx
<Slide>
  <Heading>Bilde fra nettet</Heading>
  <Image 
    src="https://placekitten.com/800/600" 
    width="800px" 
    height="600px" 
  />
</Slide>
```

---

## 4. Avanserte Funksjoner

Her er noen ting du kan gjøre for å ta presentasjonen til neste nivå.

### Vise Kode (CodePane)
Hvis du skal presentere kode, er `CodePane` fantastisk. Den gir deg syntaks-utheving (syntax highlighting).

```jsx
import { CodePane } from 'spectacle';

const minKode = `
function heiVerden() {
  console.log("Hei, verden!");
}
`;

// Inni en <Slide>:
<Slide>
  <Heading>Kodeeksempel</Heading>
  <CodePane language="javascript" showLineNumbers={false}>
    {minKode}
  </CodePane>
</Slide>
```

### Animere elementer (Appear)
Du kan få elementer til å dukke opp ett etter ett ved å bruke `<Appear>`-komponenten.

```jsx
import { Appear, ListItem, UnorderedList } from 'spectacle';

// Inni en <Slide>:
<Slide>
  <Heading>Viktige punkter</Heading>
  <UnorderedList>
    
    <Appear>
      <ListItem>Punkt nummer 1 dukker opp først</ListItem>
    </Appear>
    
    <Appear>
      <ListItem>Deretter kommer punkt nummer 2</ListItem>
    </Appear>
    
    <Appear>
      <ListItem>Og til slutt nummer 3</ListItem>
    </Appear>

  </UnorderedList>
</Slide>
```

### Layout med Grid
Spectacle har også en `<Grid>`-komponent for mer avansert plassering.

```jsx
import { Grid, Box, Text } from 'spectacle';

<Slide>
  <Grid gridTemplateColumns="1fr 1fr" gridColumnGap={15}>
    <Box backgroundColor="primary" padding={10}>
      <Text>Venstre side</Text>
    </Box>
    <Box backgroundColor="secondary" padding={10}>
      <Text>Høyre side</Text>
    </Box>
  </Grid>
</Slide>
```

### Endre Tema (Theme)
Du kan tilpasse farger og fonter ved å sende et `theme`-objekt til `<Deck>`.

```jsx
const customTheme = {
  colors: {
    primary: '#03A9F4', // Hovedtekstfarge
    secondary: '#E91E63', // Overskrifter
    tertiary: '#ffffff', // Bakgrunnsfarge
    quaternary: '#CECECE' // Sekundær tekstfarge
  },
  fonts: {
    header: '"Helvetica Neue", Helvetica, Arial, sans-serif',
    text: '"Open Sans", sans-serif'
  }
};

// <Deck theme={customTheme}> ... </Deck>
```
