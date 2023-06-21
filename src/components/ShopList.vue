<template>
    <section>
        <h3>Cart shop</h3>
        <ShopListItem v-for="item in items" 
            :itemId="item.itemId"
            :filePath="item.filePath"
            :itemTitle="item.itemTitle"
            :itemDescription="item.itemDescription"
            :itemPrice="item.itemPrice"
            @delete="(itemId: Number) => deleteItem(itemId)" />
    </section>
</template>

<script setup lang="ts">
    import { ref } from 'vue'
    import ShopListItem from '@/components/ShopListItem.vue'
    var i = 0

    const items = ref([
        {
            itemId: 1,
            itemTitle: "Item1",
            filePath: "path",
            itemDescription: "lorem lipsum",
            itemPrice: 10.0
        },
        {
            itemId: 2,
            itemTitle: "Item2",
            filePath: "path",
            itemDescription: "lorem lipsum",
            itemPrice: 100.0
        },
        {
            itemId: 3,
            itemTitle: "Item3",
            filePath: "path",
            itemDescription: "lorem lipsum",
            itemPrice: 1.0
        },
        {
            itemId: 4,
            itemTitle: "Item4",
            filePath: "path",
            itemDescription: "lorem lipsum",
            itemPrice: 12.0
        }
    ])

    function deleteItem(itemId: Number) {
        console.log(itemId);
        
        items.value = items.value.filter(item => item.itemId != itemId)
    }

</script>

<style scoped>
    section h3 {
        text-align: center;
    }
</style>
