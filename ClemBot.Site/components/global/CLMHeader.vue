<template>
  <header class="clm-header">
    <div class="clm-header__brand">
      <NuxtLink to="/">
        <img src="ClemBotLogo.png" alt="ClemBot logo" />
      </NuxtLink>
      <div class="clm-header__div">
        <CLMNavbar :trigger="isNavbarOpen" />
      </div>
    </div>
    <div class="clm-header__div">
      <CLMButton type="text icon-only" icon="discord" />
      <CLMButton type="text icon-only" icon="github" />
      <div v-if="!$auth.loggedIn" @click="login">
        <CLMButton type="filled">Login</CLMButton>
      </div>
      <div v-else>
        <GuildDropdown />
        <UserDisplay />
      </div>
      <div @click="isNavbarOpen = !isNavbarOpen">
        <CLMButton
          class="clm-js-navbar__trigger"
          type="text icon-only"
          :icon="isNavbarOpen ? 'close' : 'menu'"
        />
      </div>
    </div>
  </header>
</template>

<script>
import GuildDropdown from '~/components/GuildDropdown'
import UserDisplay from '~/components/UserDisplay'
import CLMButton from '~/components/global/CLMButton'
import CLMNavbar from '~/components/global/CLMNavbar'
export default {
  name: 'CLMHeader',
  components: { CLMNavbar, CLMButton, UserDisplay, GuildDropdown },
  data() {
    return {
      isNavbarOpen: false,
    }
  },
  methods: {
    async login() {
      await this.$auth.loginWith('discord')
    },
  },
}
</script>

<style lang="scss" scoped>
@use '~@matteusan/sentro' with (
  $prefix: 'clm',
  $context: 'token'
);
@use '../../assets/css/helpers';

@use 'sass:map';

.clm-header {
  width: 100%;
  height: auto;
  display: flex;
  flex-flow: row nowrap;
  justify-content: space-between;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 100;
  padding: 0.7rem 1rem;
  background: sentro.token-get('surface');
  color: sentro.token-get('surface-ink');

  .clm-header__brand {
    width: 100%;
    max-width: max-content;
    flex-basis: 100%;
    position: relative;

    img {
      width: 80px;
      height: 80px;
      position: absolute;
      z-index: 101;
    }
  }

  .clm-header__div {
    display: flex;
    flex-flow: row nowrap;
    flex-basis: max-content;
    justify-content: center;
    align-items: center;

    > * + * {
      margin-left: 0.7rem;
    }

    > div {
      width: 100%;
      display: grid;
      place-items: center;
    }

    &:first-child {
      justify-content: flex-start !important;
    }

    &:last-child {
      justify-content: flex-end !important;
    }
  }

  .clm-js-navbar__trigger {
    @include helpers.breakpoint('md') {
      display: none;
    }
  }
}
</style>
