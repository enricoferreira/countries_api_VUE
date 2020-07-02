<template>
    <div v-if="paises != false" class="segments">
        <div v-if="paises != false" class="segment">
            <div class="head-segment">
                <div class="d-flex align-base">
                    <h3 class="header p-r-1">America</h3>
                    <div class="input-filter p-r-1">
                        <input class="p-r-1" @change="orderList" type="radio" checked value="crescente" name="order"
                            id="azFilter">
                        <label for="azFilter">A - Z</label>
                    </div>
                    <div class="input-filter">
                        <input class="p-r-1" @change="orderList" type="radio" name="order" value="desc" id="zaFilter">
                        <label for="zaFilter">Z - A</label>
                    </div>
                </div>
                <span v-if="paises != false">
                    <h4 class="badge badge-info">{{paises.length}} Countries</h4>
                </span>
            </div>
            <list-item :paises="paises"></list-item>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Segments',
    props: ['continentes'],
    components: {
        ListItem: ()=>import('./ListItem.vue')
    }
}
</script>

<style>

</style>