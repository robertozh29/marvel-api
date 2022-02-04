<template>
  <div class="home">
    <form @submit.prevent="apiCall">
      <label for="input-1">Find your favorite marvel character</label>
      <input type="text" placeholder="Character" id="input-1" v-model="character">
      <button type="submit">Search</button>
    </form>

    <img v-if="img" alt="Character logo" :src="img">
    <div v-else class="pre">
      <p>The character search has to have the next format:</p>
      <ul>
        <li>Full name with spaces</li>
        <li>No abbrevations</li>
        <li>English names</li>
        <li>Don't the article 'the'</li>
      </ul>
      <i>There are characters like: spiderman, that wont show up because of copyrights or API records</i>
    </div>
  </div>
</template>

<script>
// ts: 1
// Public key: 432a5a46f203913911135c4accec3a14
// Private key: d91cf0759cbff952115965dd6a4aa9c655dc7140
// String: 1d91cf0759cbff952115965dd6a4aa9c655dc7140432a5a46f203913911135c4accec3a14
// Hash: 

export default {
  name: 'Home',
  components: {

  },
  data(){
    return{
      character: '',
      accessHash: 'ts=1&apikey=432a5a46f203913911135c4accec3a14&hash=341c41503a596deefc5e2ff9e8b1117f',
      img: ''
    }
  },
  methods:{
    async apiCall(){
      try{
        const call = await fetch(`http://gateway.marvel.com/v1/public/characters?name=${this.character}&${this.accessHash}`)
        const response = await call.json();
        console.log(response.data)
        this.img = response.data.results[0].thumbnail.path + '.jpg'
      }catch(error){
        console.log(error)
      }
    }
  }
}
</script>

<style>
form{
  width: 300px;
  margin: 15px auto;
}

form label{
    display: block;
    margin-bottom: 2px;
}

form input[type="text"]{
  width: 75%;
}

form button{
  width: 20%;
}



img{
  width: 300px;
  height: 300px;
}

.pre{
  margin: 50px auto;
  width: 320px;
  text-align: center;
  font-size: 14px;
}

li{
  text-align: left;
}

i{
  color: #888;
}
</style>