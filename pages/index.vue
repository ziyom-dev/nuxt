<template>
  <!-- <section>
      <div id="carouselExampleIndicators" class="carousel slide onmalika-carousel">
        <div class="carousel-indicators onmalika-carousel-controls">
          <button type="button" data-bs-target="#carouselExampleIndicators" data-bs-slide-to="0" class="active"
            aria-current="true" aria-label="Slide 1"></button>
          <button type="button" data-bs-target="#carouselExampleIndicators" data-bs-slide-to="1"
            aria-label="Slide 2"></button>
          <button type="button" data-bs-target="#carouselExampleIndicators" data-bs-slide-to="2"
            aria-label="Slide 3"></button>
        </div>

        <div class="carousel-inner">


          <div class="carousel-item  onmalika-carousel-item active">
            <img  src="/img/carousel-bg.jpg" class="w-100 bg-img" alt="">
          </div>
          <div class="carousel-item  onmalika-carousel-item">
            <img  src="https://placehold.co/1920x500?text=Баннер" class="w-100 bg-img" alt="">
          </div>
          <div class="carousel-item  onmalika-carousel-item">
            <img  src="/img/carousel-bg.jpg" class="w-100 bg-img" alt="">
          </div>


        </div>


        <button class="carousel-control-prev" style="opacity: 1;" type="button"
          data-bs-target="#carouselExampleIndicators" data-bs-slide="prev">
          <span class="dark-cover">
            <img  src="/img/arrow-left.svg" alt="">
          </span>
        </button>
        <button class="carousel-control-next" style="opacity: 1;" type="button"
          data-bs-target="#carouselExampleIndicators" data-bs-slide="next">
          <span class="dark-cover">
            <img  src="/img/arrow-right.svg" alt="">
          </span>
        </button>
      </div>
    </section>  -->
  <section class="padding-y brand-section">
    <div class="container">
      <h2>Популярные брэнды</h2>
      <div class="row row-cols-5">
        <BrandMainBrands v-for="brand in brands.results" :key="brand.id" :brand_info="brand" />
      </div>
    </div>
  </section>
  <section>
    <div class="container">
      <div class="row justify-content-between">
        <div class="col-3">
          <h2>Новинки</h2>
        </div>
        <div class="col-2">
          Controls
        </div>
      </div>
      <div class="row">
        <div class="col-lg-3 col-md-6 col-sm-6" v-for="product in products.results" :key="product.id">
          <Card :product_info="product" />
        </div>

      </div>
    </div>
  </section>
  <section>
    <img src="https://placehold.co/1920x500?text=Баннер" class="w-100" alt="" />
  </section>

  <section class="padding-y">
    <div class="container">
      <h2>
        Товары брэнда {{ getChosenBrand.name }}
      </h2>
      <div class="row row-cols-4">
        <div class="col" v-for="product in getChosenBrandProducts.results" :key="product.id">
          <Card :product_info="product" />
        </div>
      </div>
    </div>
  </section>
  <section>
    <div class="container">
      <h2>Популярные товары</h2>
      <IndexCategoryTabs :category_list="categories" />
    </div>
  </section>
</template>
  
<script setup>
const { data: products } = await useJsonPlaceholderData('/products/?limit=8')
const { data: brands } = await useJsonPlaceholderData('/brands/?limit=7')
const getBrandId = 'lg'
const { data: getChosenBrand } = await useJsonPlaceholderData('/brands/' + getBrandId)
const { data: getChosenBrandProducts } = await useJsonPlaceholderData('/products/?brand_slug=' + getBrandId + '&limit=8')
const getCategoryId = ref(99)
const categories = ref([]);
const { data: getChosenCategory } = await useJsonPlaceholderData('/categories/?parent=' + getCategoryId.value);
if (getChosenCategory.value && getChosenCategory.value.results) {
  for (const category of getChosenCategory.value.results) {
    const { data: getChosenCategoryProducts } = await useJsonPlaceholderData(`/products/?category=${category.id}&limit=7`);
    if (getChosenCategoryProducts.value) {
      category.products = getChosenCategoryProducts.value;
    }
  }
  categories.value = getChosenCategory.value.results;
}
</script>
<style lang="scss">
.page-enter-active,
.page-leave-active {
  transition: all 0.3s;
}

.page-enter-from,
.page-leave-to {
  opacity: 0;
  filter: blur(1rem);
}
</style>
  
