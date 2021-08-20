<template>
<div class="container">
  <div class="upvote-list">
     <div class="upvote-card">
      <div :key="index" class="upvote-card rating" v-for="(rating , index) in item.count">
          <div v-bind:class="{'selected': item.selected , 'not-selected': !item.selected }" class="upvote-card image-container" @click="changeBackgroudColor">
              <img :src="item.img" class="upvote-card image" :key="item.id" :alt="'filled image'" :aria-hidden="true" />
           </div>
      </div>
    </div>
  </div>
  <div class="upvote-buttons">
    <button class="button-update"  @click="addRate">
      <img src="src/assets/add-filled.svg" aria-hidden="true" title="button image"/>
    </button>
  </div> 
</div>
</template>
<script>



import Vuex from 'vuex';

const store = new Vuex.Store({
  state: {
    rating:[],
  }, getters: {
    getRating: state => {
      return state.rating;
    }
  },
  mutations:{
    addRating: (state, item) => {
      state.rating.push(item);
    },
    addRate: (state, item) => {
      state.rating.forEach(e => {
         if(item.id === e.id){
           e.count = e.count + 1
         }
      })

    },

    changeColor(state , payload) {
      state.rating.forEach(e => {
         if(payload === e.id){ // toogles the state from selected to not-selected
            e.selected = !e.selected;
         }
      })
    }
  }
});

export default {
  name: 'UpVote',
  store,
  props: {
    upvote: Object
  },
  mounted() {
    store.commit('addRating' , this.$props.upvote);
  },
  beforeDestroy() {
    // this.sub();
  },
  data() {
    return {
      item: this.$props.upvote,
      appliedStyles:{
        backgroundColor: this.$props.normal
      },
      ratings: store.getters.getRating
    }
  },
  methods: {
    addRate(){
      this.item.count = this.item.count + 1
      store.commit('addRate' , this.item.id);
    },
    changeBackgroudColor(event) {
      store.commit('changeColor' , this.item.id);
    }
  }

}
</script>
