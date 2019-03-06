<template>
  <div>
   <b-row>
        <b-col deck v-for="(m, index) in photo" :key="index" cols="3" class="pad" >
          <b-card-group > 
            <b-card 
              v-bind:title="m.al"
              v-bind:img-src="m.url"
              img-alt="Image"
              img-top
              tag="article"
              style="max-width: 20rem; "
              
            >
               
            </b-card>
            
          </b-card-group>
          
        </b-col>
        
      </b-row>
</div>
</template>

<script>
import axios from "axios";
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return{
      photo: [] 
    }
    
  },
  mounted() {
    axios
      .get("http://jsonplaceholder.typicode.com/photos")
      .then(response => {
        console.log(response);
        const data = response.data;

        for (let key in data) {
          const datapho = data[key];
          datapho.id = key;
          this.photo.push({
            al:datapho.albumId,
            id:datapho.id,
            title:datapho.title,
            url:datapho.url

        });
          console.log(this.photo.albumId);
        }
      })
      .catch(error => {
        console.log(error);
      });
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
