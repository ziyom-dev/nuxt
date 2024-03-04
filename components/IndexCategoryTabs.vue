<template>
    <div class="category-tablist">

        <div class="row">
            <div class="col-6">
                <ul class="nav nav-pills onmalika-index-categories mb-3" id="pills-tab" role="tablist">
                    <li class="nav-item" v-for="(cat, index) in category_list" :key="cat.id" role="presentation">
                        <button class="nav-link btn-success btn" :class="{ 'active': index == 0 }"
                            :id="`pills-category-tab${index}`" data-bs-toggle="pill"
                            :data-bs-target="`#pills-category${index}`" type="button" role="tab"
                            :aria-controls="`pills-category${index}`" aria-selected="true">{{ cat.name
                            }}</button>
                    </li>
                </ul>
            </div>
        </div>
        <div class="tab-content" id="pills-tabContent">
            <div class="tab-pane fade" :class="{ 'active show': index == 0 }" v-for="(cat, index) in category_list"
                :key="cat.id" :id="`pills-category${index}`" role="tabpanel"
                :aria-labelledby="`pills-category-tab${index}`">
                <div class="grid-parent">
                    <div :class="'grid-' + number" v-for="(product, number) in cat.products.results" :key="product">
                        <MiniCard :product_info="product" />
                    </div>
                </div>

            </div>

        </div>

    </div>
</template>

<script setup>
const props = defineProps({
    category_list: {
        type: Object,
        required: true,
    },
});
const { category_list } = props;
</script>
