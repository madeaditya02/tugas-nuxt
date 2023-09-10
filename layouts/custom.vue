<template>
    <div>
        <Header />
        <Nuxt />
        <Footer />
    </div>
</template>
<script>
import Header from '../components/header.vue'
import Footer from '../components/header.vue'
export default {
    layouts: { Header, Footer }
}
</script>  