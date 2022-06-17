<script>
import Facultets from '../assets/faculties.js';
export default {
  data() {
    return {
      Facultets,
      selectedFacultets:[],
      sort_initial: 'id',
      sort_selected: 'id'
    };
  },
  methods: {
      deleteNote(index, array) { 
        if(array === 'Facultets'){
          return this.Facultets.splice(index, 1);
        }
        return this.selectedFacultets.splice(index, 1);
      },

      compare_name(a, b) {
        if (a.data.name < b.data.name)
          return -1;
        if (a.data.name > b.data.name)
          return 1;
        return 0;
      },

      compare_id(a, b) {
        if (a.data.id < b.data.id)
          return -1;
        if (a.data.id > b.data.id)
          return 1;
        return 0;
      },

      sortedArray(array) {
        if(array === 'Facultets'){
            var sort_initial = this.sort_initial
            var sort_array = this.Facultets
        }else{
            var sort_initial = this.sort_selected
            var sort_array = this.selectedFacultets
        }
        if(sort_initial === 'name'){
          return sort_array.sort(this.compare_name);
        }
        return sort_array.sort(this.compare_id);
        
      },

    }
}
</script>

<template>
  <main>
    <ul class="lists_facultet">
      <div class="sort_btn">
        <button :class="{'activ_btn' : sort_initial === 'id', 'pass_btn' : sort_initial === 'name'}" @click="this.sort_initial = 'id'">ID</button>
        <button :class="{'pass_btn' : sort_initial === 'id', 'activ_btn' : sort_initial === 'name'}" @click="this.sort_initial = 'name'">Имя</button>
      </div>
      <span v-if="Facultets.length">
        <li v-for="(facultet, index) in sortedArray('Facultets')" :key="index">
          <input type="checkbox" v-model="selectedFacultets" :value="facultet" @change="deleteNote(index, 'Facultets')">
          <p>{{facultet.data.id}}</p>
          <p>{{facultet.data.name}}</p>
        </li>
      </span>
      <p class="empty_list" v-else>Список пуст</p>
    </ul> 
    
    <ul class="lists_facultet">
      <div class="sort_btn">
        <button :class="{'activ_btn' : sort_selected === 'id', 'pass_btn' : sort_selected === 'name'}" @click="this.sort_selected = 'id'">ID</button>
        <button :class="{'pass_btn' : sort_selected === 'id', 'activ_btn' : sort_selected === 'name'}" @click="this.sort_selected = 'name'">Имя</button>
      </div>
      <span v-if="selectedFacultets.length">
        <li v-for="(facultet, index) in sortedArray('selectedFacultets')" :key="index">
            <input type="checkbox" v-model="Facultets" :value="facultet" checked @change="deleteNote(index)">
            <p>{{facultet.data.id}}</p>
            <p>{{facultet.data.name}}</p>
        </li>
      </span>
      <p class="empty_list" v-else>Список пуст</p>
    </ul>
  </main>
</template>

<style>

  main{
    display: flex;
    justify-content: space-around;
    align-items: start;
    padding: 50px;
  }
  .lists_facultet{
    list-style-type: none;
    width: 45%;
  }
  .lists_facultet li{
    border-top:1px solid rgb(177, 177, 177) ;
    display: flex;
    align-items: center;
    gap:25px;
  }
  .sort_btn{
    padding: 0 0 10px 36px;
    display: flex;
    gap: 30%;
  }

  .empty_list{
    display: flex;
    justify-content: center;
  }

  .activ_btn{
    color: #4b5266;
    background: #a3d7dd;
    border: 1px solid #4b5266;
    border-radius: 5px;
    padding: 5px 15px;
  }

  .pass_btn{
    background: #fff;
    border: 1px solid #757880;
    border-radius: 5px;
    color: #757880;
    padding: 5px 15px;
  }
</style>