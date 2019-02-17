<template>
  <div :class="$style.home">
    <stage :disable-particles="disableParticles" />
  </div>
</template>

<script lang="ts">
import { mapState } from 'vuex';
import Stage from '../Stage/Stage.vue';
import { IState } from '../../state';

export default {
  metaInfo: {
    title: 'Trivia 2019',
    meta: [
      {
        name: 'description',
        content:
          'vue-starter - The most complete boilerplate for production-ready PWAs. With focus on performance, development speed, and best practices',
      },
      {
        name: 'robots',
        content: 'INDEX,FOLLOW',
      },
      {
        name: 'keywords',
        content: 'vue.js, vuex, vuex-persist, seo, server-side-rendering, isomorphic, progressive-web-app',
      },

      { name: 'og:url', content: 'https://vue-starter.herokuapp.com/' },
      { name: 'og:site_name', content: 'vue-starter' },
      { name: 'og:type', content: 'website' },
      { name: 'og:locale', content: 'en' },
      {
        name: 'og:title',
        content:
          'vue-starter - The most complete boilerplate for production-ready PWAs. With focus on performance, development speed, and best practices',
      },
      {
        name: 'og:description',
        content:
          'vue-starter - The most complete boilerplate for production-ready PWAs. With focus on performance, development speed, and best practices',
      },
      { name: 'og:image:url', content: 'https://vue-starter.herokuapp.com/logo.png' },

      { name: 'twitter:card', content: 'summary' },
      { name: 'twitter:site', content: '@_jwerner_' },
      { name: 'twitter:creator', content: '@_jwerner_' },
      {
        name: 'twitter:title',
        content:
          'vue-starter - The most complete boilerplate for production-ready PWAs. With focus on performance, development speed, and best practices',
      },
      { name: 'twitter:url', content: 'https://vue-starter.herokuapp.com/' },
      { name: 'twitter:image', content: 'https://vue-starter.herokuapp.com/logo.png' },
      {
        name: 'twitter:description',
        content:
          'vue-starter - The most complete boilerplate for production-ready PWAs. With focus on performance, development speed, and best practices',
      },
    ],
  },
  components: {
    Stage,
  },
  computed: {
    ...mapState({
      disableParticles: (state: IState) => state.app.config && state.app.config.features.disableParticles,
    }),
  },
};
</script>

<style lang="scss" module>
@import '../../shared/design-system';

.home {
  h2 {
    line-height: 1.2;
  }

  :global {
    .vueCard {
      height: 100%;
      padding: $space-unit * 2;
    }

    .vueGridItem {
      margin-bottom: $space-unit * 2;
    }

    .featureSection {
      padding: 0;
    }
  }

  @include mediaMin(tabletLandscape) {
    :global {
      .featureSection {
        padding: $space-unit * 15 0;
      }
    }
  }
}
</style>
