<template>
  <div class="home">
    <form @submit.prevent="validate">
      <label for="input-1">Find your favorite marvel character</label>
      <input type="text" placeholder="Character" id="input-1" v-model.trim="name">
      <button type="submit">Search</button>
    </form>

    <character-card 
      v-if="search" 
      :name="this.character.name"
      :img="this.character.thumbnail.path + '.' + this.character.thumbnail.extension"
    />
    <div v-else class="pre">
      <p>Character search must have the next format:</p>
      <ul>
        <li>Full name with spaces</li>
        <li>No abbrevations</li>
        <li>Don't use the article 'the'</li>
        <li>Only english names</li>
      </ul>
      <i>There are characters like: spiderman, that wont show up because of copyrights or API records</i>
    </div>
  </div>
</template>

<script>
import CharacterCard from '../components/CharacterCard.vue'
// ts: 1
// Public key: 432a5a46f203913911135c4accec3a14
// Private key: d91cf0759cbff952115965dd6a4aa9c655dc7140

export default {
  name: 'Home',
  components: {
    CharacterCard
  },
  data(){
    return{
      accessHash: 'ts=1&apikey=432a5a46f203913911135c4accec3a14&hash=341c41503a596deefc5e2ff9e8b1117f',
      name: '',
      character: {},
      search: false
    }
  },
  methods:{
    async apiCall(){
      try{
        const call = await fetch(`http://gateway.marvel.com/v1/public/characters?name=${this.name}&${this.accessHash}`)
        const response = await call.json();
        if(response.data.total > 0){
          this.character = response.data.results[0];
          this.search = true
        }else{
          this.search = false
        }
      }catch(error){
        console.log(error)
      }
    },
    validate(){
      if(this.name != ''){
        this.apiCall()
      }
    }
  }
}
</script>

<style scoped>
.home{
  width: 350px;
  margin: auto; 
  display:flex;
  flex-direction:column;
  align-items: center;
}
form{
  width: 100%;
  margin: 15px;
}
form label{
    display: block;
    margin-bottom: 5px;
}
form input[type="text"]{
  width: 80%;
  box-sizing: border-box;
  padding: 3px 10px;
}
form button{
  width: 20%;
  padding: 3px 0;
}

.pre{
  margin: 10px auto;
  width: 320px;
  text-align: center;
  font-size: 14px;
}
.pre p{
  font-size: 16px;
  margin-bottom: 5px;
}

.pre ul{
  padding-left:25px;
  padding-bottom: 15px;
}
li{
  text-align: left;
}

i{
  color: #888;
}
</style>