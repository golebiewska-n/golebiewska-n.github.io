<template>
  <nav>
    <RouterLink to="/">
      portfolio
    </RouterLink>
    <RouterLink to="/contact">
      contact
    </RouterLink>
    <a
      class="instagram-link"
      href="https://instagram.com/nati.krati"
      target="_blank"
    >
      <img src="/src/assets/img/instagram.png">
    </a>
  </nav>
</template>

<script>
import { RouterLink } from 'vue-router'

export default {
  components: {
    RouterLink
  }
}
</script>

<style scoped lang="scss">
  nav{
    display: flex;
    flex-direction: column;
    @media (max-width: 960px) {
      flex-direction: row;
      justify-content: center;
    }
    a{
      margin-bottom: 15px;
      text-decoration: none;
      color: #000;
      @media (max-width: 960px){
        margin-right: 30px;
        margin-bottom: 40px;
      }
      &.router-link-active{
        font-weight: 400;
      }
    }
    .instagram-link{
      width: 14px;
      margin-top: 20px;
      @media (max-width: 960px){
        margin-top: 1.5px;
      }
      img{
        width: 100%;
      }
    }
  }
</style>
