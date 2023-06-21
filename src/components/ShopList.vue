<template>
    <section>
        <ShopListItem v-for="item in items" 
            :filePath="item.filePath"
            :itemTitle="item.itemTitle"
            :itemDescription="item.itemDescription"
            :itemPrice="item.itemPrice" />
    </section>
</template>

<script setup lang="ts">
    import { ref } from 'vue'
    import ShopListItem from '@/components/ShopListItem.vue'

    const items = ref([
        {
            itemTitle: "Item1",
            filePath: "path",
            itemDescription: "lorem lipsum",
            itemPrice: 10.0
        },
        {
            itemTitle: "Item2",
            filePath: "path",
            itemDescription: "lorem lipsum",
            itemPrice: 100.0
        },
        {
            itemTitle: "Item3",
            filePath: "path",
            itemDescription: "lorem lipsum",
            itemPrice: 1.0
        },
        {
            itemTitle: "Item4",
            filePath: "path",
            itemDescription: "lorem lipsum",
            itemPrice: 12.0
        }
    ])

</script>

<style scoped>

</style>
