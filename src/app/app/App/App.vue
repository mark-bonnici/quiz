<template>
  <div id="app" :class="$style.app">
    <vue-notification-stack />

    <router-view :class="$style.content" />

    <vue-footer />
  </div>
</template>

<script lang="ts">
import { mapActions, mapGetters } from 'vuex';
import VueNavBar from '../../shared/components/VueNavBar/VueNavBar.vue';
import VueGrid from '../../shared/components/VueGrid/VueGrid.vue';
import VueGridItem from '../../shared/components/VueGridItem/VueGridItem.vue';
import { loadLocaleAsync } from '../../shared/plugins/i18n/i18n';
import VueSidebar from '../../shared/components/VueSidebar/VueSidebar.vue';
import VueSidebarGroup from '../../shared/components/VueSidebar/VueSidebarGroup/VueSidebarGroup.vue';
import VueSidebarGroupItem from '../../shared/components/VueSidebar/VueSidebarGroupItem/VueSidebarGroupItem.vue';
import VueIconCode from '../../shared/components/icons/VueIconCode/VueIconCode.vue';
import VueIconBook from '../../shared/components/icons/VueIconBook/VueIconBook.vue';
import VueIconHashtag from '../../shared/components/icons/VueIconHashtag/VueIconHashtag.vue';
import VueIconGithub from '../../shared/components/icons/VueIconGithub/VueIconGithub.vue';
import VueIconTwitterSquare from '../../shared/components/icons/VueIconTwitterSquare/VueIconTwitterSquare.vue';
import VueSelect from '../../shared/components/VueSelect/VueSelect.vue';
import VueIconPuzzlePiece from '../../shared/components/icons/VueIconPuzzlePiece/VueIconPuzzlePiece.vue';

const fetch = require('node-fetch');
const quizData = 'https://api.myjson.com/bins/ahn1p';

export default {
  name: 'App',
  components: {
    VueIconPuzzlePiece,
    VueSelect,
    VueIconHashtag,
    VueIconBook,
    VueIconCode,
    VueGrid,
    VueGridItem,
  },
  computed: {
    ...mapGetters('app', ['cookieConsentVersion', 'getLocale']),
  },
};
</script>

<style lang="scss" module>
@import '../../shared/design-system';
@import '../../shared/designSystem/reset';
@import '../../shared/designSystem/typo';
@import '../../shared/designSystem/global';

.app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.content {
  flex: 1;
}
</style>
