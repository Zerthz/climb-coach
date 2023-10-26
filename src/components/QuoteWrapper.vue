<template>
    <div>
        <Quote @current-quote="recieveQuote"/>
    </div>
</template>

<script>
import CopyToClipboard from './CopyToClipboard.vue';
import Quote from './Quote.vue';

export default {
    components: { Quote },
    
}
</script>
<style lang="">
    
</style>