<template>
  <div class="container cat-game-wrap">
    <div class="row align-items-center">
      <div class="col-md-6">
        <div class="row">
          <div class="col-xs-3" v-for="(cat,index) in Cats" :key="index">
            <div class="cat-img-wrap">
              <img v-bind:src="'./img/cats/' + cat" class="img-responsive cat-img" @click="fillGridItem(cat, index)" />
            </div> 
          </div>
        </div>
      </div>
      <div class="col-md-6">
        <h2 class="text-center">CATS GRID</h2>
        <div class="grid-wrap">
          <div class="grid-box" v-for="(grid, index) in grids" :key="index">
            <img v-if="grid && grid.img" v-bind:src="'./img/cats/' + grid.img" class="grid-cat img-responsive" /> 
          </div>
        </div>
        <div class="text-center" v-if="fillIndex == 12">
          <button type="button" @click="reset()" class="btn btn-primary">Reset Grid</button>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped>
  .cat-game-wrap{
    font-size: 16px;
  }
  .cat-img-wrap{
    margin-bottom:20px;
  }
  .cat-img{
    height:200px;
    cursor:pointer;
  }
  .grid-box{
    border: 1px solid #33bb4f;
    width: 33.33%;
    height: 100px;
    display: block;
    margin: 0;
    float: left;
  }
  .grid-cat{
    height: 80px;
    margin: 10px auto;
  }
</style>
<script>
import Vue from 'vue';
export default {
  /**
   * The name of the page.
   */
  name: 'HomeIndex',

  /**
   * The components that the page can use.
   */
  components: {
  },
  data() {
    return {
      fillIndex:0,
      grids: new Array(12),
      Cats: ['cat_1.png','cat_2.png','cat_3.png','cat_4.png','cat_5.png','cat_6.png','cat_7.png','cat_8.png','cat_9.png','cat_10.png','cat_11.png','cat_12.png']
    }
  },
  mounted() {
    this.grids.fill({img:'', index:null});
  },
  methods : {
    fillGridItem(cat, index) {
      if(this.fillIndex < 12){
        Vue.set(this.grids, this.fillIndex, {img: cat, index: index})
        this.fillIndex++;
        if(this.fillIndex == 12){ // show alert
          let victory = true;
          for(let row=0;row<4 ; row++) {
            let i = row*3;
            if((this.grids[i].index == this.grids[i+1].index) || 
                (this.grids[i].index == this.grids[i+2].index) ||
                (this.grids[i+1].index == this.grids[i+2].index)
                ){
              victory = false;
              break;
            }
          }
          setTimeout(() =>{
            alert(victory ? 'YOU WIN' : 'YOU LOSE');
          }, 250);
        }
      }
    },
    reset() {
      this.fillIndex = 0;
      this.grids.fill({img:'', index:null});
    }
  }
};
</script>
