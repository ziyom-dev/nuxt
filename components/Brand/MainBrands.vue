<template>
    <div class="col mb-4">
        <NuxtLink :to="'/brands/' + brand_info.slug" class="brand-main">
            <!-- <img  :src="'http://64.23.130.79:8000' + brand_info.image.url" alt="" /> -->
            <h4>{{ brand_info.name }}</h4>
        </NuxtLink>
    </div>
</template>

<script setup>
const props = defineProps({
    brand_info: {
        type: Object,
        required: true,
    },
});
const { brand_info } = props;
</script>

