<template>
  <section class="hero">
    <div class="hero__media">
      <img id="main-logo" src="ClemBotLogo.png" alt="ClemBot" />
    </div>
    <div class="hero__content">
      <div class="hero__header">
        <h1>ClemBot</h1>
        <p>
          The modular and configurable open source Discord Bot for all your
          needs.
        </p>
      </div>
      <div class="hero__actions">
        <a
          href="https://discord.com/api/oauth2/authorize?client_id=710672266245177365&permissions=398828104950&scope=bot"
        >
          <CLMButton label="Summon me!" type="filled raised" icon="discord" />
        </a>
      </div>
    </div>
  </section>
</template>

<script lang="ts">
import CLMButton from '~/components/global/CLMButton.vue'
export default {
  name: 'Hero',
  components: { CLMButton },
}
</script>

<style lang="scss" scoped>
@use '~@matteusan/sentro' with (
  $prefix: 'clm',
  $context: 'token'
);

.hero {
  width: 100%;
  display: flex;
  flex-flow: column nowrap;
  padding: 100px 0 2rem 0;

  .hero__media {
    width: 120px;
    height: 120px;
    margin: 0 auto;

    img {
      width: 100%;
      height: 100%;
    }
  }

  .hero__content {
    padding: 0 1rem;

    .hero__header {
      text-align: center;

      h1,
      h2,
      h3 {
        font-size: 3rem;
        font-weight: 700;
        text-align: inherit;
        text-shadow: -2px 2px sentro.token-get('primary-dark'),
          -3px 3px sentro.token-get('primary'),
          -4px 5px sentro.token-get('primary-light');
      }

      p {
        font-size: 1.2rem;
        text-shadow: -1px 1px sentro.token-get('primary-dark');
      }
    }

    .hero__actions {
      width: 100%;
      margin-top: 1rem;
      gap: 0.5rem;
      text-align: center;
    }
  }
}
</style>
