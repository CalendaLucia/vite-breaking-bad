<script>
    import AppHeader from './components/AppHeader.vue';
    import AppMain from './components/AppMain.vue';
    import axios from 'axios';
    import {store} from './store';
    export default {
        name:'App',
            components: {
            AppHeader,
            AppMain,
        },
        data() {
            return {
                store,
                selected:''
            };
        },

        mounted() {
          this.getArchetypes();
        },
        watch: {
          selected: function() {
             this.getCards();
            },
        },
        methods: {
            cards() {
            axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php').then((response) => {
                this.store.cards = response.data.data.slice(0,20);
                this.store.loaded = true;
            });   
         },
          getArchetypes() {
             axios.get('https://db.ygoprodeck.com/api/v7/archetypes.php')
            .then(response => {
                store.archetypes = response.data;store.ok = true;
       })
           .catch(error => {
              console.error(error);
        });
 
         },
          getCards() {
            if (!this.selected) {
                    axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php', {
                        params: {
                            archetype: this.selected,
                        }
                    }).then((response) => {
                        this.store.cards = response.data.data.slice(0,50);
                    });
                }
                else {
                    this.Cards();
                }
        },
    }
         
}

        
        
</script>

<template>
    <AppHeader/>
    <AppMain/>
</template>

<style  lang="scss">
@import "./styles/main.scss";
</style>