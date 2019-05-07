<template>
  <div id="app">
    <div class="container" id="container">
      <div class="row">
        <div class="col">
          <quote-tracker :itemsAdded="total_quotes"></quote-tracker>
        </div>
      </div>

      <div class="row">
        <div class="col-md-6 offset-md-3">
          <form>

            <textarea 
              class="editor"
              ref="editor"></textarea>

            <button 
              class="add-quote btn btn-primary"
              @click.prevent="addQuote">
              Add Quote
            </button>
          </form>
        </div>
      </div>

      <div class="row justify-content-center quotes" v-if="quotes.length > 0">
        <div class="col-md-3"  v-for="(quote, index) in quotes" :key="index">
          <div class="quote" @click="removeItem(index)">
            {{ quote }}
          </div>
        </div>
      </div>

      <div class="row text-center quotes" v-else>
        <div class="col">
          <h3>No quotes added</h3>
        </div>
      </div>

      <footer class="row alert alert-info">
        Info: Click on a quote to delete quote.
      </footer> 
    </div>  
  </div>
</template>



<script>
  import Tracker from './components/Tracker.vue'

  export default {

    data(){
      return {

        quotes: []
      }
    },


    components: {
      'quote-tracker': Tracker
    },


    methods: {
      

      /**
       * Funtion adds data in textarea (editor) to the
       * list of quotes
       * 
       *
       */
      addQuote(){
        var newQuote = this.$refs.editor.value;

        if(newQuote.trim() !== ''){
          this.quotes.unshift(newQuote);
          this.$refs.editor.value = '';
          this.$refs.editor.focus();
        }
      },



      /**
       * Function is called a quote is clicked.
       * It removes a quote from existing quotes
       * 
       * @param { Number } index
       */
      removeItem( index ){
        this.quotes.splice(index, 1);
      }
    },


    computed: {
      total_quotes(){
        return parseInt(this.quotes.length);
      }
    }
  }
</script>



<style>
  #container {
    position: relative;
  }

  form {
    text-align: center;
  }

  .editor, .add-quote {
    display: block;
    margin: 15px auto 30px;
  }
  .editor {
    padding: 6px 10px;
    width: 100%;
    height: 30vh;
    box-sizing: border-box;
  }

  .add-quote {
    padding: 5px 30px;
    border-radius: 5px;
    box-sizing: border-box;

    border: none;
  }

  .btn-primary {
    background:   rgb(21, 106, 180);
  }

  .quotes {
    min-height: 30vh;
    color: rgb(165, 161, 161);
  }

  .quote {
    color: rgb(53, 53, 53);
    min-height: 130px;
    margin: 20px auto;
    border-radius: 10px;
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.25);

    padding: 15px;
  }

  .quote:hover {
    cursor: pointer;
  }



</style>