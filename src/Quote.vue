<template>
    <div class="quote" @click="removed(item)">
        <p>{{ quote }}</p>
    </div>
</template>
<script>
    export default {
        props: ['quote','removed', 'item']
    }
</script>