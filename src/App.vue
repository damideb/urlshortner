<template>
  <div class="title">
    <h1 class="brandName"> Linkly </h1>
    <SectionOne/>
  </div>
  <ShortenView />
  <AdvancedView/>

  <div class="last-section">
    <div class="boost">
      <h2>Boost your links today</h2>
      <button>Get Started</button>
    </div>

    <div class="footer">
      <h1 class="Name">Linkly</h1>

      <div class='tableDiv'>
        <div>
          <h4>Features</h4>
          <p> Link Shortening</p>
          <p>Branded Links</p>
          <p>Analytics</p>
        </div>

        <div>
          <h4>Resource</h4>
          <p> Blog</p>
          <p>Developers</p>
          <p>Support</p>
        </div>

        <div>
          <h4>Company</h4>
          <p> About</p>
          <p>Team</p>
          <p>Careers</p>
          <p>Contact</p>
        </div>

      </div>
    </div>
  </div>
</template>

<script>
  import SectionOne from '@/components/SectionOne.vue'
  import ShortenView from '@/components/ShortenView.vue'
  import AdvancedView from '@/components/AdvancedView.vue'


export default {
  name: 'App',

  components:{
    SectionOne,
    ShortenView,
    AdvancedView
  },



}
</script>

