<template>
    <div class="big-box">
        <!-- COPERTINA -->
        <div class="cover-container">
            <img class="cover" :src="'/storage/' + arrDishes.cover_image" alt="logo" onerror="this.src='../../../storage/placeholder.jpeg';">
        </div>

        <!-- LOGO -->
        <div class="logo-box">
            <div class="logo-container">
                <img class="logo" :src="'/storage/' + arrDishes.logo_image" alt="logo" onerror="this.src='../../../storage/placeholder.jpeg';">
            </div>
        </div>
        <div class="restaurant-name-container">
            <h1 class="restaurant-name-vue">{{ arrDishes.name }}</h1>
            <div class="categories-container">
                <div v-for="category in arrDishes.categories" :key="category.id" class="category-tag">
                    {{ category.name }}
                </div>
            </div>
        </div>
        <div class="cards-container">
            <div class="rounded-4 my-card"
            v-for="dish in arrDishes.dishes" :key="dish.id">
                <div v-if="dish.visible==true" class="dish-img-container rounded-4"><img :src="'/storage/' + dish.image" alt="image" onerror="this.src='../../../storage/placeholder.jpeg';" class="rounded-4 dish-img"></div>
                <div v-else class="dish-img-container rounded-4"><img :src="'/storage/' + dish.image" alt="image" style="filter: grayscale(100%);" onerror="this.src='../../../storage/placeholder.jpeg';" class="rounded-4 dish-img"></div>
                <div class="dish-name">{{ dish.name }}</div>
                <div class="dish-info">{{ dish.description }}</div>
                <div class="dish-price"><span style="color: #00ccbb ;">&euro;</span> {{ dish.price }}</div>
                <div v-if="dish.visible==true" class="dish-button-container">
                    <button class="dish-button" @click="$emit('addCart', dish)"> Aggiungi al carrello</button>
                </div>
                <div v-else class="dish-button-container">
                    <button class="dish-button" style="filter: grayscale(100%);" disabled> Piatto non disponibile</button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
    export default {
        name: 'PageDishes',
        props: [
        'slug',
        ],

        data(){
            return {
                arrDishes:[],
            }
        },

        created(){
            axios.get('/api/dishes/' + this.slug)
                .then(response => this.arrDishes = response.data.results);
                console.log(this.arrDishes);
        },


    }
</script>
<style lang="scss">

    .logo-box{
        width: 100%;
        display: flex;
        justify-content: center;
    }

   .logo-container{
    border-radius: 50%;
    width: 350px;
    height: 350px;
    background-size:cover;
    background-position:center center;
    background-repeat:no-repeat;
    border: solid #00ccbb 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
    background-color: white;
    position: absolute;
    margin: -200px;
   }

   .logo{
    width: 100%;
   }

   .cover-container{
    width: 100%;
    height: 500px;
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    overflow: hidden;
   }

   .cover{
    width: 100%;
   }

   .cards-container{
    display: flex;
    flex-wrap: wrap;
    width: 100%;
    align-items: center;
    justify-content: center;
    position: relative;
    margin-bottom: 50px;
   }

   .my-card{
    margin: 2rem;
    display: flex;
    flex-direction: column;
    overflow: hidden;
    height: 500px;
    width: 300px;
    position: relative;
    border: 2px solid #00ccbb;
    font-size: 0.8rem;
    line-height: 20px;
   }

   .dish-img-container{
    display: flex;
    justify-content: center;
    align-items: center;
    overflow: hidden;
    height: 50%;
    width: 102%;
    position: relative;
    right: 1%;
   }
   .dish-img{
    height: 100%;

   }
   .dish-name{
    text-align: center;
    font-size: 2em;
    padding-top: 10px;
    height: 10%;
    // background-color: red;
   }

   .dish-info{
    font-size: 1.5em;
    padding: 5px 15px;
    height: 15%;
    // background-color: blue;
   }

   .dish-price{
    font-size: 2em;
    padding-top: 25px;
    padding-left: 15px;
    height: 15%;
    // background-color: green;
   }

   .dish-button-container{
    text-align: center;
    height: 10%;
    // background-color: yellow;
   }

   .dish-button{
    background-color: #00ccbb;
    width: fit-content;
    border-radius: 20px;
    color: white;
    border: none;
    padding: .5rem 1rem;
    white-space: nowrap;
    font-size: 1.5em;
    box-shadow: 3px 3px #888888;
   }
   .dish-button:hover{
    background-color: white;
    color: black;
   }

   .restaurant-name-vue{
    font-size: 3em;
    margin-top: 175px;
    margin-bottom: 25px;
    text-align: center;
   }

   .categories-container{
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
   }

   .category-tag{
    padding: .5rem 1rem;
    background-color: #00ccbb;
    width: fit-content;
    border-radius: 15px;
    margin-top: 20px;
    margin-right: .5rem;
    font-size: 2em;
   }

   @media (max-width: 390px){
    .logo-container{
    border-radius: 50%;
    width: 200px;
    height: 200px;
    margin: -200px;
   }

   .restaurant-name-vue{
    margin-top: 25px;
   }

   }
</style>
