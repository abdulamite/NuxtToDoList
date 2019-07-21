<template>
  <div class="container">
    <div>
      <ListContainer/>
    </div>
  </div>
</template>

<script>
import ListContainer from '~/components/ListContainer.vue'

export default {
  components: {
    ListContainer
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  justify-content: center;
  align-items: center;
  text-align: center;
  display: grid; 
  grid-template-columns: 1fr 2fr 1fr;
  grid-template-rows: 1fr; 
  grid-column-gap: 0px;
  grid-row-gap: 0px; 
}

.container>div{
  grid-column-start: 2;
  background-color: #F5F5F5;
  height: 100%;
}



.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}

@media (min-width: 481px) and (max-width: 767px) {
  .container {
  grid-template-columns: 1fr;
}
.container>div{
  grid-column: 1/-1;
}
  
}

/* 
  ##Device = Most of the Smartphones Mobiles (Portrait)
  ##Screen = B/w 320px to 479px
*/

@media (min-width: 320px) and (max-width: 480px) {
  .container {
  grid-template-columns: 1fr;
  grid-gap: 0;
  width:100%;
}
.container>div{
  grid-column: 1/-1;

}
  

}



</style>
