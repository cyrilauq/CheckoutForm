<template>
    <div>
        <img :src="filePath" />
        <div>
            <h4>{{ itemTitle }}</h4>
            <p>{{ itemDescription }}</p>
            <p>{{ itemPrice }} €</p>
        </div>
    </div>
</template>

<script setup lang="ts">
    import { ref } from 'vue'

    const props = defineProps({
        filePath: String,
        itemTitle: String,
        itemPrice: Number,
        itemDescription: String
    })
</script>

<style scoped>
    div {
        display: flex;
        flex-direction: row;
    }
    img {
        width: 100px;
        height: 60px;
        margin-top: auto;
        margin-bottom: auto;
        margin-right: 15px;
    }
    div > div {
        display: flex;
        flex-direction: column;
    }
    p, h4 {
        margin: 0;
    }
</style>