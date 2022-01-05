<template>
  <nav :class="`clm-navbar${trigger ? ' open' : ''}`">
    <ul class="clm-navbar__wrapper">
      <li class="clm-navbar__item">
        <NuxtLink to="/" active-class="active">
          <p>Home</p>
        </NuxtLink>
      </li>
      <li class="clm-navbar__item">
        <NuxtLink to="/wiki" active-class="active">
          <p>Wiki</p>
        </NuxtLink>
      </li>
      <li class="clm-navbar__item">
        <NuxtLink to="/status" active-class="active">
          <p>Status</p>
        </NuxtLink>
      </li>
      <li class="clm-navbar__item">
        <NuxtLink to="/support" active-class="active">
          <p>Support</p>
        </NuxtLink>
      </li>
    </ul>
  </nav>
</template>

<script lang="ts">
export default {
  name: 'CLMNavbar',
  props: {
    trigger: {
      default: false,
      type: Boolean,
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

.clm-navbar {
  width: 250px;
  height: calc(100% - 57px);
  display: none;
  position: fixed;
  bottom: 0;
  right: 0;
  z-index: 99;
  padding: 1rem;

  background-color: sentro.key-create(
    'navbar-fill',
    sentro.token-get('surface-dark')
  );
  color: sentro.key-create('navbar-ink', sentro.token-get('surface-ink'));
  border: 1px solid
    sentro.key-create('navbar-border', sentro.token-get('surface-dark'));

  @include helpers.breakpoint('md') {
    width: 100%;
    height: auto;
    display: flex !important;
    flex-flow: row nowrap;
    position: relative;
    left: 90px;
    padding: 0;
    color: inherit;
    @include sentro.key-bind('navbar-fill', rgba(0 0 0 / 0));
    @include sentro.key-bind('navbar-border', rgba(0 0 0 / 0));
  }

  &.open {
    display: flex;
    flex-flow: column nowrap;
    @include sentro.elevation-apply(4);

    @include helpers.breakpoint('md', $context: 'max') {
      .clm-navbar__wrapper {
        & > * + * {
          margin-top: 0.7rem;
        }
      }
    }
  }

  .clm-navbar__wrapper {
    display: inherit;
    flex-flow: inherit;
    justify-content: inherit;
    align-items: inherit;

    .clm-navbar__item {
      width: 100%;
      padding: 0.4rem 0.6rem;
      display: flex;
      flex-flow: row nowrap;
      justify-content: flex-start;
      align-items: center;
      color: #fff;
      border: 1px solid rgba(0 0 0 / 0);
      border-radius: 0.3rem;

      @include helpers.breakpoint('md') {
        justify-content: center;
      }

      &:hover {
        background: rgba(255 255 255 / 20%);
        border: 1px solid rgba(255 255 255 / 2%);
      }

      .active {
        border-bottom: 2px solid sentro.token-get('secondary');

        > * {
          border-bottom: 2px solid sentro.token-get('secondary');
        }
      }
    }
  }
}
</style>
