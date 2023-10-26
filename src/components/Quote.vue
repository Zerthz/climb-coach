<template>
    <div class="container">
        <h2>Klättercoachen</h2>
        <blockquote class="text-center">{{text}}</blockquote>
        <p>- Klättercoachen🧗</p>
        <div class="buttons">
            <button class="btn-secondary" @click="newQuote">Coach Me</button>
            <button class="btn-secondary" @click="copyToClipboard">Copy To Clipboard</button>
        </div>
    </div>
</template>



<script>
    import quotes from '../data/quotes'

    export default{
        data() {
            return{
                quotes,
                text: '',
                usedQuotes: []
            }
        },
        methods:{
            newQuote(){
                let arr = this.quotes;
                if(quotes.length === 0){
                    console.log("resetting");
                    this.quotes = this.usedQuotes;
                    arr = this.usedQuotes;
                }
                let randomIndex = Math.floor(Math.random() * (quotes.length - 0) + 0);
                let item = arr[randomIndex];
                this.text = arr[randomIndex].quote;
                this.usedQuotes.push(item);
                this.quotes.splice(randomIndex, 1);
                this.$emit('current-quote', this.text + ' - Klättercoachen 2023')
            },
            async copyToClipboard(){
                try{
                    let textToCopy = '🧗\"' +  this.text + '\" -Klättercoachen 2023🧗'
                    await navigator.clipboard.writeText(textToCopy);
                    console.log('copied to clipboard');
                }
                catch(err){
                    console.log('Failed to copy: ', err)
                }
            }
        },
        beforeMount(){            
            this.newQuote()
        }
       
       
    }
    
</script>

<style scoped>
    h2{
        font-family: 'Roboto';
        font-size: 2.25rem;
        border-bottom: 1px solid var(--clr-secondary);
        padding-bottom: .25em;
    }
    p{
        font-family: 'Roboto';
        font-size: 1.2rem;
        font-style: italic;
    }
    .container{
        display: flex;
        flex-direction: column;
        place-items: center;
        gap: 1em;
    }

    .buttons{
        display: flex;
        gap: 2rem;
    }

    @media (min-width: 640px) {
        blockquote::after{
            bottom:0;
        }        
    }
    @media(min-width: 1000){
        blockquote::after{
            bottom:-50%;
        }   
    }
   

   
</style>