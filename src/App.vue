<template>
  <div id="app">
    <div class="container">
      <h2>Quotes App</h2>
        <div class="bar">
            <span :style="{ width: (quotes.length/10) * 100 + '%' }">{{ (quotes.length/10) * 100 }}%</span>
        </div>
      <div class="row">
        <div class="col-lg-5">
          <form action="">
            <textarea v-model="quote" cols="30" rows="10"></textarea>
            <button @click.prevent="addQuote">Add Quote</button>
          </form>
          <div class="alert alert-info" role="alert">
            Click On  a Quote to Delete
          </div>

        </div>
        <div class="col-lg-7">
          <quote v-for="(quote, item) in quotes" :key="item" :quote="quote" :item="item" :removed="removeQuote"></quote>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import Quote from './Quote.vue';
export default {
  name: 'app',
  data () {
    return {
        quotes:[
            '"Moral indignation is jealousy with a halo."',
            '"Glory is fleeting, but obscurity is forever."'
        ],
        quote:'',
    }
  },
    components: {
      quote: Quote,
    },
    methods:{
      addQuote(){
          if(this.quotes.length == 10){
              return alert('You can Only Add 10 Quotes, Please remove some.');
          }
          if (this.quote.length == 0) {
              return alert('Please Enter A Quote');
          }
          this.quotes.push(this.quote);
          this.quote = '';
      },
        removeQuote(event){
            this.quotes.splice(event,1);
            this.updateProgress();
        }
    },
    mounted(){
      this.size = (this.quotes.length/10) * 100;
      console.log('mounted ' + this.size);
    }
}
</script>
<style>
  textarea{
    width: 100%;
    border: 1px solid #ccc;
    padding: 20px;
  }
  button{
    background: #999;
    border: none;
    color: #fff;
    width: 100%;
    margin: 10px 0;
    padding: 10px;
    font-family: 'Oswald', sans-serif;
    text-transform: uppercase;
  }
  button:focus, button:hover{
      background: #666;
      outline: none;
  }
  div.quote{
    padding: 20px;
    text-align: center;
    font-style: italic;
    margin: 0 0 20px 0;
    border:1px dashed #ccc;
    color: #999;
  }
  div.quote:hover{
      color: #000;
      cursor: hand;
  }
  h2{
    padding: 30px;
    margin: 0;
    background: #ccc;
    color: #999;
    text-transform: uppercase;
    margin: 15px 0;
    font-family: 'Oswald', sans-serif;
    font-weight: 700;
      border-radius: 10px;
  }
    div.bar span {
        display: block;
        background: #888;
        height: 30px;
        margin-bottom: 15px;
        border-radius: 5px;
        text-align: center;
        color: #fff;
        line-height: 30px;
        font-weight: bold;
    }
</style>
