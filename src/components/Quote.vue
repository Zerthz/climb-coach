<template>
    <div class="container">
        <h2>Klättercoachen</h2>
        <blockquote class="text-center">{{text}}</blockquote>
        <p>- Klättercoachen🧗</p>
        <div class="buttons">
            <button class="btn-secondary" @click="newQuote">Coach Me</button>
            <button class="btn-secondary" @click="copyToClipboard">Copy To Clipboard</button>
            
        </div>
        <Transition name="fade">
            <p v-show="copied">Copied to clipboard</p>
        </Transition>
    </div>
</template>



<script>
    import quotes from '../data/quotes'

    export default{
        data() {
            return{
                quotes,
                text: '',
                usedQuotes: [],
                copied: false
            }
        },
        methods:{
            async remove(){
                await setTimeout(() => this.copied = false, 2000);
                
            },
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
                    this.copied= true;
                    // setTimeout(this.copied = false, 200000)
                    await this.remove()
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

    .fade-enter-active{
        animation: fade-in 4s;
    }
    .fade-leave-active {
        display: none;
    }

    @keyframes fade-in{
        0%{
            opacity: 0;
        }
        25%{
            opacity: 1;
        }
        100%{
            opacity: 0;
        }
    }

    .v-enter-from,
    .v-leave-to {
    opacity: 0;
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