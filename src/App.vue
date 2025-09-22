<template>
  <v-app>
    <header>

    </header>
    <body>
      <h1>Application de Dactylographie</h1>
      <p>Les mots a saisir : {{ lesMots }}</p>
      <input v-model="texte" placeholder="Enter texte" />
      <button @click="demarrer()">Démarrer</button>
      <p> Temps : {{ temps }}</p>
      <p> Char/sec : {{ charactereParSeconde }}</p>
    </body>
    <footer>

    </footer>
  </v-app>
</template>

<script setup>

  import { ref } from 'vue'
  const texte = ref('')
  const temps = ref (0)
  const motASaisir = ref('')
  const charactereParSeconde = ref('')
  let enMarche = false
  let intervalID1 = setInterval(() => {})
  let intervalID2 = setInterval(() => {})
  let lesMots = ''
  const mots = [
    'chat',
    'manger',
    'oiseau',
    'pain',
    'fromage',
    'maison',
    'voiture',
    'fleur',
    'arbre',
    'livre',
    'école',
    'stylo',
    'fenêtre',
    'porte',
    'chien',
    'plage',
    'montagne',
    'soleil',
    'lune',
    'rivière',
  ]

  /**
   * Ajoute 1 a la variable temps
   */
  function compteur () {
    temps.value++
  }

  /**
   * Commence le Timer
   */
  function demarrer () {
    // appel la fonction compteur toute les 1000 milisecondes (1 seconde)
    if (!enMarche) {
      texte.value = ''
      temps.value = 0
      intervalID1 = setInterval(compteur, 1000)
      intervalID2 = setInterval(RegarderSiReussi, 100)
      mettreMots()
      enMarche = true
    }
  }

  function arreter () {
    clearInterval(intervalID1)
    clearInterval(intervalID2)
    enMarche = false
  }

  function SaisirUnMot () {
    motASaisir.value = mots[Math.floor(Math.random() * mots.length)]
  }

  function mettreMots () {
    lesMots = ''
    for (let i = 0; i < 10; i++) {
      SaisirUnMot()
      lesMots += motASaisir.value + ' '
    }
  }
  function RegarderSiReussi () {
    const saisieSansEspace = texte.value.replaceAll(' ', '')
    const motsSansEspace = lesMots.replaceAll(' ', '')
    charactereParSeconde.value = (lesMots.length / temps.value).toFixed(2)
    if (saisieSansEspace === motsSansEspace) {
      arreter()
    }
  }
</script>
<style scoped>
/* Structure principale : occupe toute la hauteur de l'écran */
.v-app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  background-color: #ffffff;
}

/* Header et Footer : bandes bleues */
header, footer {
  background-color: #0053ff;
  color: white;
  text-align: center;
  padding: 1.5rem;
  flex-shrink: 0;
}

/* Corps principal : tout le contenu */
body {
  flex: 1;
  background-color: #ffffff;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  margin: 0;
  padding: 2rem;
  color: #000000;
}

/* Zone de texte */
input {
  color: black;
  padding: 12px;
  width: 400px;
  font-size: 20px;
  margin-bottom: 1.5rem;
  border: 2px solid #000;
  border-radius: 5px;
}

/* Bouton stylé vert */
button {
  background-color: #57ff00;
  color: white;
  padding: 12px 24px;
  font-size: 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  margin-left: 1rem;
}

button:hover {
  background-color: #333333;
}

/* Textes */
p {
  font-size: 24px;
  margin: 15px 0;
}

h1 {
  font-size: 32px;
  margin-bottom: 1.5rem;
}

</style>
