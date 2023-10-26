<template>
    <div>
        <Quote @current-quote="recieveQuote"/>
    </div>
</template>

<script>
import Quote from './Quote.vue';

export default {
    components: { Quote },
    
}
</script>
<style lang="">
    
</style>