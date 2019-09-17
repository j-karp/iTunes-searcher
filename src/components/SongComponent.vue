<template>
    <div class="SongComponent" v-if="song.wrapperType != 'audiobook'">
  
      <!-- Obraz albumu -->
      <img :src="song.artworkUrl60" alt="Image"/>

      <!-- Szczegóły utworu: tytuł + nazwa artysty -->
      <p v-if="song.trackName && song.artistName"> 
        <!-- Skrócenie nazwy utworu jeśli jest zbyt długa -->
        <b v-if="song.trackName.length < 50">{{song.trackName}}</b>
        <b v-else>{{song.trackName.substring(0,50) + "..."}}</b>
        <br />
        <!-- Skrócenie nazwy artysty jeśli jest zbyt długa -->
        <a v-if="song.artistName.length < 20">{{"By " + song.artistName}}</a>
        <a v-else>{{"By " + song.artistName.substring(0,20) + "..."}}</a>
      </p>
    
    </div>
</template>


<script>
export default {
  name: "SongComponent",
  props: ["song"],
};
</script>,


<style scoped>
.SongComponent {
  display: inline-block;
  width: 200px;
  height: 80px;
  color: #000000;
  background: #ebebde;
  margin: 5px;
  box-sizing: border-box;
  cursor: pointer;
}

.SongComponent img {
  padding: 10px 0 10px 10px;
  float: left;
}

.SongComponent:hover{
  border: 1px #ff6600 solid;
   -moz-box-shadow:     0 0 10px #000000;
   -webkit-box-shadow:  0 0 10px #000000;
   box-shadow:          0 0 10px #000000;
}

.SongComponent p {
  padding: 2px;
  height: 80px;
  width: 130px;
  display: table-cell;
  vertical-align: middle;
}
</style>
