<template>
  <footer class="clm-footer">
    <section class="clm-footer__wrapper">
      <div class="clm-footer__header">
        <h2>ClemBot</h2>
        <p>Copyright &copy; {{ new Date().getFullYear() }} - CCS</p>
      </div>
      <div class="clm-footer__actions">
        <NuxtLink :to="{ path: '/privacy' }">Privacy Policy</NuxtLink>
      </div>
    </section>
  </footer>
</template>
<script>
export default {
  name: 'CLMFooter',
}
</script>

<style lang="scss" scoped>
@use '~@matteusan/sentro' with (
  $prefix: 'clm',
  $context: 'token'
);

.clm-footer {
  width: 100%;
  padding: 1.2rem;
  background: sentro.token-get('surface-light');
  color: sentro.token-get('surface-ink');
  text-align: center;

  .clm-footer__wrapper {
    width: calc(100% - 30px);
    max-width: 1077px;
    margin: 0 auto;

    .clm-footer__header {
      text-align: center;
    }

    .clm-footer__actions {
      display: flex;
      flex-flow: row wrap;
      justify-content: center;
      align-items: center;
      gap: 0.7rem;
      margin-top: 0.9rem;

      a:hover {
        color: sentro.token-get('primary');
      }

      .clm-button--icon-only {
        color: #fff !important;
      }
    }
  }
}
</style>
