<template>
  <div>
    <section class="hero__wrapper has-shadow">
      <Hero />
    </section>
    <section class="content-wrap">
      <section class="stats-card__wrapper">
        <h2 class="title">Features</h2>
      </section>
      <section class="feature-card__wrapper">
        <FeatureCard
          v-for="feature in features"
          :key="feature.title"
          :title="feature.title"
          :description="feature.description"
          :image="feature.image"
        />
      </section>
    </section>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import FeatureCard from '~/components/home/FeatureCard.vue'
import Hero from '~/components/home/Hero.vue'
// import Stats from '~/components/home/Stats.vue'

export default Vue.extend({
  components: {
    // Stats,
    Hero,
    FeatureCard,
  },
  middleware: 'HomeAuthCheck',
  data() {
    return {
      guildsCount: 'Unknown',
      usersCount: 'Unknown',
      commandsCount: 'Unknown',

      features: [
        {
          title: 'Message Logging',
          description:
            'Complete message edit and deletion logging to make moderating easy.',
          image: 'FeatureImages/MessageEdit.png',
        },
        {
          title: 'Moderation',
          description:
            'Ban troublesome members, mute spammers, and keep track of warnings to provide some accountability in your community.',
          image: 'FeatureImages/MemberMute.png',
        },
        {
          title: 'User Logging',
          description:
            "Keep track of your servers' joins and leaves with welcome messages and logging posts.",
          image: 'FeatureImages/UserJoinEmbed.png',
        },
        {
          title: 'Custom Tags',
          description:
            'Create custom tags and invoke them later to easily convey repeated information or just an inside joke.',
          image: 'FeatureImages/TagInvoke.png',
        },
        {
          title: 'Assignable Roles',
          description:
            'Set roles as assignable, and allow your members to self assign what roles they want.',
          image: 'FeatureImages/AssignRoles.png',
        },
        {
          title: 'Custom Prefixes',
          description:
            "Do you have multiple bots in your server? Clembot's command prefix is completely customizable!",
          image: 'FeatureImages/CustomPrefix.png',
        },
      ],
    }
  },

  async fetch() {
    const stats = await this.$api.public.getGlobalStats()

    if (stats === null) {
      console.log('Getting public guild stats failed')
      return
    }

    this.guildsCount = stats.guilds ?? 'many'
    this.usersCount = stats.users ?? 'all the'
    this.commandsCount = stats.commands ?? 'tons of'
  },
})
</script>

<style lang="scss" scoped>
.hero__wrapper {
  width: 100%;
  background-image: url('static/SplashBkg.svg');
  background-repeat: no-repeat;
  background-position: bottom;
  background-size: cover;
  user-select: none;
  transform: translateZ(0);
  -webkit-transform: translateZ(0);
  box-shadow: rgba(0, 0, 0, 0.35) 0 5px 15px;
}

.stats-card__wrapper {
  display: flex;
  flex-flow: column nowrap;
  align-items: center;

  .stats-card__explainer {
    text-align: center;
  }
}

.title {
  font-size: 32px;
  margin: 1.3rem 0;
  font-weight: 700;
}

.feature-card__wrapper {
  width: 100%;
  display: grid;
  grid-template-columns: repeat(1, 1fr);
  margin-bottom: 0.7rem;
  gap: 0.7rem;

  @media (min-width: 640px) {
    grid-template-columns: repeat(2, 1fr);
  }

  @media (min-width: 877px) {
    grid-template-columns: repeat(3, 1fr);
  }
}
</style>
