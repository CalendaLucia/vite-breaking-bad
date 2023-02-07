<script>
import {store} from '../store';
    export default {
        name:'AppMain',
        data() {
            return {
                store,
           
           
            };
        },
       
    }
</script>

<template>
   <div class="container-fluid p-5 bg-warning">
     <div class="input-group mb-3 p-3 ">
       <select v-model="selected" class="custom-select border-light px-3" id="inputGroupSelect01">
          <option v-for="archetype in store.archetypes" :value="archetype.archetype_name ">
            {{ archetype.archetype_name }}
          </option>
       </select>
     </div>
     <div class="container mb-4 w-75 px-4 py-3 mx-auto bg-white">
        <div class="spinner-border text-warning" role="status" v-if="this.store.loaded ==false">
           <span class="sr-only ">Loading...</span>
        </div>
        <div class="row"> 
            <div class="col-3 bg-black mb-1" v-for="card in store.cards">
                <img class="img-fluid" :src="card.card_images[0].image_url_small" :alt="card.name">
            </div>
        </div>
     </div>
   </div>
</template>

<style lang="scss">

</style>
