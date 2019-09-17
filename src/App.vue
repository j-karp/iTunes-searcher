
// TODO
// Zgodnie z założeniem - aplikacja po kliknięciu przycisku search pobiera 9 piosenek,
// stąd też suma pobranych piosenek = 9 (lub mniej).
// Należy sprawdzić wartość liczby wszystkich możliwych wyników i wyświetlić prawdziwą 
// wartość.
// Mając tę wartość trzeba też ograniczyć offset z góry, aby paginacja nie działała 
// w nieskończoność do przodu.

// Z API iTunes można pobrać max. 200 wyników i wyświetlić komunikat (np. znaleziono 
// 200+ piosenek) ale to się mija z powyższym założeniem.


<template>
  <div id="app">  

    <!-- Import czcionki: Lato -->
    <link rel="stylesheet" type="text/css" href="//fonts.googleapis.com/css?family=Lato" />
    
    <!-- Nagłówek zawierający logo -->
    <div id="header">
    <a href="."><img alt="PGS logo" src="./assets/logo.png"></a>
    </div>
  
    <!-- Sekcja wyszukiwania zawierająca pasek szukania -->
    <div class="searchingSection">
      <h1>iTunes api example</h1>
      <div class="searchBar">
        <input type="text" class="searchTerm" id="search_request" placeholder="Search songs...">
        <button type="submit" class="searchButton" v-on:click="direction = true; offset = 0; send_request(); ">search</button>
      </div>
      <p>
        Search by song title, author, song number, lyric, catalog or copyright owner
      </p>
    </div>

    <!-- Komponent wyświetlania wyników   -->
    <ResultsSection v-if="search_response" v-bind:results="search_response" />

    <!-- Przyciski przewijania   -->
    <div class="scrollButtonsContainer" v-if="search_response.results && search_response.results.length != 0">
      <button type="submit" class="scrollButton" v-on:click="direction = false; offset -= 9; send_request()">prev</button>
      <button type="submit" class="scrollButton" v-on:click="direction = true; offset += 9; send_request()">next</button>
    </div>

    <!-- Stopka -->
    <div id="footer">
      Powered by PGS
    </div>

  </div>
</template>


<script>
import ResultsSection from './components/ResultsSection.vue'

export default {
  name: 'app',
  components: {
    ResultsSection
  },
  data() {
    return {
      search_request: "",
      search_response: "",
      offset: 0,
      direction: true,
    }
  },
  methods: {
    get_request: function () {
      this.search_request = document.getElementById("search_request").value
          .trim()
          .replace(/ /g, "+")
          .toLowerCase()
    },

    send_request: function () {
      this.get_request()

      if (this.offset < 0) this.offset = 0
      //TODO: Ograniczyć offset z góry

      var url = "https://itunes.apple.com/search?"
                + "limit=9"
                + "&entity=song"
                + "&wrapperType=track"
                + "&offset=" + this.offset
                + "&term=" + this.search_request

      fetch(url)
      .then(resp => resp.json())
      .then(resp => { 
        this.search_response = resp
      })
    }
  }
}
</script>


<style>
#app {
  font-family: 'Lato', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #ffffff;
}

img{
  margin: auto;
  max-width: 105px;
  max-height: 70px;
}

#header {
  max-width: 655px;
  margin: auto;
  background: #ffffff;
  text-align: left;
}

.searchingSection {
  background: #303030;
  padding: 15px;
}

.searchBar {
  min-width: 165px;
  width: 30%;
  position: relative;
  display: flex;
  margin: auto;
}

.searchTerm {
  width: 100%;
  border: 0px ;
  padding: 5px;
  height: 20px;
  border-radius: 30px 0 0 30px;
  outline: none;
  text-indent: 10px;
  margin: 15px 0px 15px 0px;
}

.searchButton {
  max-width: 80px;
  min-width: 50px; 
  width: 30%;
  padding: 5px;
  border: 0px solid #00B4CC;
  background: #ff6600;
  text-align: center;
  color: #fff;
  border-radius: 0 30px 30px 0;
  cursor: pointer;
  margin: 15px 0px 15px 0px;
}

.scrollButtonsContainer {
  padding-bottom: 40px;
}

.scrollButton {
  max-width: 80px;
  min-width: 50px; 
  width: 30%;
  padding: 5px;
  border: 0px solid #00B4CC;
  background: #ff6600;
  text-align: center;
  color: #fff;
  border-radius: 30px 30px 30px 30px;
  cursor: pointer;
  margin: 5px;
}

#footer {
  background: #303030;
  padding: 10px;
  font-size: 11px;
}

/* Kod CSS dla czcionki Lato */
h1 { 
  font-family: Lato; 
  font-size: 20px; 
  font-style: normal; 
  font-variant: normal; 
  font-weight: 700; 
  line-height: 26.4px; 
} 

h3 { 
  font-family: Lato; 
  font-size: 14px; 
  font-style: normal; 
  font-variant: normal; 
  font-weight: 700; 
  line-height: 15.4px; 
} 

p { 
  font-family: Lato; 
  font-size: 10px; 
  font-style: normal; 
  font-variant: normal; 
  font-weight: 400; 
  line-height: 20px; 
} 

blockquote { 
  font-family: Lato; 
  font-size: 21px; 
  font-style: normal; 
  font-variant: normal; 
  font-weight: 400; 
  line-height: 30px; 
} 

pre { 
  font-family: Lato; 
  font-size: 13px; 
  font-style: normal; 
  font-variant: normal; 
  font-weight: 400; 
  line-height: 18.5714px; 
}
</style>
