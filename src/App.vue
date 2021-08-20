<template>
<ul class="votes">
  <li class="votes list" v-for="upvote in upvotes" :key="upvote.id">
    <up-vote :upvote="upvote"></up-vote>
  </li>
</ul>
</template>

<script>
import UpVote from './components/UpVote.vue'

export default {
  name: 'App',
  components: {
    UpVote
  },

  data() {
    return{
      upvotes: [
        { id: 1, label: 'Default', count: 3 , img:'src/assets/Arrow+Tail-Up.svg' , selected: false },
        { id: 2 , label: 'Normal', count: 2 , img:'src/assets/Arrow+Tail-Up-Blue.svg' , selected: false },
        { id: 3, label: 'Fill',  count: 5 , img:'src/assets/Arrow+Tail-Up-Red.svg' , selected: false }
      ]
    } 
  }
}
</script>
