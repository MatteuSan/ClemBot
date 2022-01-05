<template>
  <div>
    <CLMHeader />
    <main>
      <nuxt v-if="!$slots.default" />
      <slot />
    </main>
    <CLMFooter />
  </div>
</template>

<script lang="ts">
import CLMHeader from '~/components/global/CLMHeader.vue'
import CLMFooter from '~/components/global/CLMFooter.vue'

export default {
  components: { CLMFooter, CLMHeader },
}
</script>

<style scoped lang="scss">
.section {
  height: 20%;
}

#main-logo {
  position: fixed;
  z-index: 200;
  min-width: 5rem;
  max-width: 6rem;
}

#discord-login {
  background: #5865f2;
  box-shadow: rgba(0, 0, 0, 0.15) 1.95px 1.95px 2.6px;
  text-decoration: none;
}

#nav {
  left: 38%;
}

#splash-card {
  opacity: 0.95;
}

#tray-icons {
  transition: all 1.2s ease-in-out;
}

#tray-icons :hover {
  transform: scale(1.1);
  color: white;
}

#socials {
  display: flex;
  align-items: center;
  justify-content: center;
}

#discord-login :hover + .animation-wrapper {
  animation-name: ckw;
  animation-duration: 1.5s;
  /* Things added */
  animation-iteration-count: infinite;
  display: inline-block;
  /* <--- */
}
@keyframes ckw {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
