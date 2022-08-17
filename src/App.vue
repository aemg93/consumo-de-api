Angel Moreno, [17/08/22 6:03 A. M.]
<template>
  <div>
    <div class="title">
     <h1> Consumo De Una Api Con <span><img class="logo" src="./assets/logo.svg" alt="logo vue" ></span>ue.JS</h1></div>
       <table>
         <tbody >
           <tr v-for="user of users" :key="user.id">
           <td class="avatar"><img :src=" user.avatar" alt="avatar">{{  }}</td>
           <td class="id">{{ user.id }}</td>
           <td class="first_name">{{ user.first_name }}</td>
           <td class="las_name">{{ user.last_name }}</td>
           <td class="las_name">{{ user.email }}</td>

      </tr>
      </tbody>
    </table>
    <div class="butto">
      <button style="margin-right: 5px" class="pagination-previous" @click="changePage( page - 1 )">anterior</button>
      <button class="pagination-link  is-current">{{ page }}</button>
      <button  style="margin-left: 6px" class="pagination-next" @click="changePage( page + 1 )">siguiente</button>
    </div>


  </div>
</template>

<script>
import axios from 'axios'
export default {
  data: function () {
    return {
      users: [],
      page: 1,
      pages: 1

    }
  },
  mounted() {
    this.getTodos();
  },
  methods: {
    getTodos() {
      const params = {
        page: this.page
      }
      axios
          .get('https://reqres.in/api/users?page/', {params})
          .then( res => {
            this.users = res.data.data
            this.pages = res.data.pages
            console.log(res.data)
          })
          .catch( e => console.log(e),


          )},
    changePage (page) {
      this.page = ( page <= 0 || page > this.pages) ? this.page : page;
      this.getTodos();
      console.log('hola desdes changrPage')
    }

  }
};

</script>

<style scoped>

.title{
  height: 100px;
  background-color: #EEE;
  display:flex;
  justify-content: center;
  align-items: center;
  margin-bottom: -40px
}
.logo{
  min-width: 96px;
  height: 58px;
  margin-top: -49px;
  margin-right: -27px;

}
.title {
  background: rgb(70,78,158);
  background: linear-gradient(90deg, rgba(70,78,158,1) 2%, rgb(35, 39, 77) 38%, rgb(28, 22, 22) 100%);

}
h1 {

    font-weight: bold;
    color: white;
    min-width: 100%;
    margin-top: 10px;
    justify-content: center;
    position: relative;
    text-align: center;
;
}
.butto {
  position: absolute;
  left: 15rem;
  margin-top: 10px

}
td {
  background-image: url("https://besthqwallpapers.com/Uploads/19-8-2020/139972/thumb2-internet-networking-blue-networks-background-communication-global-network-concepts.jpg");
  color: white;
  text-align: center;
}
img {
  max-width: 40px;
  height: 40px;
 margin-bottom: -7px;
}
table {
  justify-content: center;
  margin-top: 40px;
  width: 40rem;
  height: 2px;
  background: #6a77e1;

}
.avatar {
  width: 10px;
  border-bottom: 40px;
}
</style>