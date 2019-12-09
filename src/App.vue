<template>
  <div id="app">
    <h1>Grid</h1>
    <p>
      Lorem ipsum, dolor sit amet consectetur adipisicing elit. Optio sit sunt,
      voluptatem incidunt est perferendis architecto dolorum quasi nobis
      asperiores ratione dolores aut, voluptatibus quae? Doloremque quisquam
      eaque molestiae dolorum?
    </p>
    <p>Text is placed to show that content is showing corectly</p>

    <p>
      Also grid is fully responsive without any js, only scss, you can check it
      in Grid.vue component
    </p>

    <h3>Basic Grid</h3>
    <Grid container spacing="2">
      <Grid xs="12" sm="6" md="4" lg="2" v-for="num in 6" :key="num">
        <div class="border center padding">
          {{ num }}
        </div>
      </Grid>
    </Grid>

    <h3 class="offset-top">Nested Grid</h3>
    <Grid container spacing="2">
      <Grid xs="6">
        <Grid container spacing="2">
          <Grid xs="3">
            <div class="border center padding">small nested elem</div>
          </Grid>
          <Grid xs="3">
            <div class="border center padding">small nested elem</div>
          </Grid>
          <Grid xs="6">
            <div class="border center padding">big nested elem</div>
          </Grid>
        </Grid>
      </Grid>

      <Grid xs="6" class="rounded">
        <div class="border center padding">no nested elemes</div>
        <div class="border center padding">but with aditional class</div>
      </Grid>
    </Grid>
  </div>
</template>

<script>
import Grid from './components/Grid';

export default {
  name: 'app',
  components: {
    Grid
  }
};
</script>

<style lang="scss">
body {
  padding: 60px;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  padding: 25px;
  border: 1px solid #ccc;
}

h1,
h3 {
  text-align: center;
}

.offset-top {
  margin-top: 50px;
}

.border {
  border: 1px solid #e3e3e3;
}

.center {
  text-align: center;
}

.padding {
  padding: 8px;
}

.rounded {
  & > div {
    border-radius: 10px;
  }

  & > div:not(:last-child) {
    margin-bottom: 10px;
  }
}
</style>
