<template>
  <div class="home">
    <HeaderShayna />
    <HeroSection />
    <BannerShayna />
    <InstaShayna />
    <PartnerLogos />
    <FooterShayna />
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import HeaderShayna from '@/components/HeaderShayna.vue'
import HeroSection from '@/components/HeroSection.vue'
import BannerShayna from '@/components/BannerShayna.vue'
import InstaShayna from '@/components/InstaShayna.vue'
import PartnerLogos from '@/components/PartnerLogos.vue'
import FooterShayna from '@/components/FooterShayna.vue'


export default {
  name: 'Home',
  components: {
    HeaderShayna,
    HeroSection,
    BannerShayna,
    InstaShayna,
    PartnerLogos,
    FooterShayna
  }
}
</script>
