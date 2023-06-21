<script setup lang="ts">
    import PayementInformation from '@/components/PayementInformation.vue'
    import ShopList from '@/components/ShopList.vue'
</script>

<template>
    <div id="checkOutForm">
        <PayementInformation />
        <ShopList />
    </div>
</template>

<style scoped>
    #checkOutForm {
        display: flex;
        flex-direction: row;
    }
</style>
