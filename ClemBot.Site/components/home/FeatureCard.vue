<template>
  <div class="feature-card">
    <div>
      <h2 class="feature-card__title">{{ title }}</h2>
      <p class="feature-card__description">
        {{ description }}
      </p>
    </div>
    <div class="feature-card__media">
      <img :src="image" />
    </div>
  </div>
</template>

<script lang="ts">
export default {
  props: {
    title: {
      type: String,
      required: true,
    },
    description: {
      type: String,
      required: true,
    },
    image: {
      type: String,
      required: true,
    },
  },
}
</script>

<style lang="scss" scoped>
@use '~@matteusan/sentro' with (
  $prefix: 'clm',
  $context: 'token'
);

.feature-card {
  width: 100%;
  padding: 1.2rem;
  display: flex;
  flex-flow: column nowrap;
  justify-content: space-between;
  border-radius: 0.5rem;
  background: sentro.token-get('surface-light');
  color: sentro.token-get('surface-ink');
  @include sentro.elevation-apply(2);

  .feature-card__title {
    margin-bottom: 0.5rem;
    font-size: sentro.px-to-rem(26px);
    line-height: sentro.px-to-rem(30px);
  }

  .feature-card__description {
    font-size: sentro.px-to-rem(16px);
    line-height: sentro.px-to-rem(20px);
  }

  .feature-card__media {
    width: 100%;
    height: 100%;
    max-height: 250px;
    margin-top: 1.2rem;
    overflow: hidden;

    img {
      width: 100%;
      height: 100%;
      object-fit: contain;
      object-position: center;
    }
  }
}
</style>
