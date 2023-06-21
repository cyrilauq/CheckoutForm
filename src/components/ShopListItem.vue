<template>
    <div>
        <img :src="filePath" />
        <div>
            <h4>{{ itemTitle }}</h4>
            <p>{{ itemDescription }}</p>
            <p>{{ itemPrice }} €</p>
        </div>
        <span class="closeBtn" @click="$emit('delete', itemId)">close</span>
    </div>
</template>

<script setup lang="ts">
    import { ref, watch } from 'vue'

    const props = defineProps({
        itemId: Number,
        filePath: String,
        itemTitle: String,
        itemPrice: Number,
        itemDescription: String
    })

    const emit = defineEmits(['delete'])

    function removeItem() {
        console.log(props.itemId);
        
        emit('delete', props.itemId)
    }
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