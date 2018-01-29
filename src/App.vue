<template>
    <div class="container">
        <app-header :quoteCount= "quotes.length" :maxQuotes="maxQuotes"></app-header>
        <app-new-quote @quoteAdded="newQuote"></app-new-quote>
        <app-quote-grid :quotes="quotes" @quoteDeleted="deleteQuote"></app-quote-grid>
        <label>Max Number</label>
        <input type="text" name="quoteMaxNumber" class="form-control" @keyup ="changeMaxNumber($event.target.value)"  placeholder="please set the max number of quotes">
        <div class="row">
            <div class="col-sm-12 text-center">
                <div class="alert alert-info">Info: Click on a Quote to delete it!</div>
            </div>
        </div>
    </div>
</template>

<script>
    import QuoteGrid from './components/QuoteGrid.vue';
    import NewQuote from './components/NewQuote.vue';
    import Header from './components/Header.vue';
    export default {
        data: function () {
            return {
                quotes: [
                    'Just a Quote to see something'
                ],
                maxQuotes: 1
            }
        },
        methods: {
            newQuote(quote) {
                if (this.quotes.length >= this.maxQuotes) {
                    return alert('Please delete Quotes first!');
                }
                if (quote.length == 0) {
                    return alert('Can\'t Add  Empty Quote !');
                }
                this.quotes.push(quote);
            },
            deleteQuote(index){
                this.quotes.splice(index,1)
            },
            changeMaxNumber(number){
                if (number < 1) {
                    return alert('quotes can\'t be less than 1...');
                }
                this.maxQuotes = number
            }
        },
        components: {
            appQuoteGrid: QuoteGrid,
            appNewQuote: NewQuote ,
            appHeader:Header
                   }
    }
</script>

<style>
</style>
