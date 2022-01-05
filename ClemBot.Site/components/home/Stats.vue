<template>
  <div class="stats-card has-background-dark has-shadow">
    <h2>📊 ClemBot Stats</h2>
    <p>
      Currently running <b>{{ guildsCount }}</b> servers...
    </p>
    <p>
      Watching <b>{{ usersCount }} </b> users...
    </p>
    <p>
      And over <b>{{ commandsCount }}</b> commands handled!
    </p>
  </div>
</template>

<script lang="ts">
export default {
  name: 'Stats',
  data(): Record<string, string | Record<string, string>> {
    return {
      guildsCount: 'Unknown',
      usersCount: 'Unknown',
      commandsCount: 'Unknown',
    }
  },
}
</script>

<style lang="scss" scoped>
@use '~@matteusan/sentro';

.stats-card {
  width: calc(100% - 30px);
  max-width: 420px;
  margin: 2rem auto;
  padding: 1rem;
  border-radius: 0.5rem;
  box-shadow: -3px 3px #181818;
  // transform: skew(3deg);
  transform: rotate3d(1, 1, 1, -3.4deg);
  cursor: default;
  @include sentro.prefix(transition, all 0.1s ease);

  &:hover {
    transform: rotate3d(1, 1, 4, -1.2deg);
    box-shadow: -5px 5px #181818;
  }

  h2 {
    font-size: 1.3rem;
    font-weight: 700;
  }
}
</style>
