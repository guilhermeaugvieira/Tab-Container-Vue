<template>
  <div class="container">
    <TabContainer :activeTab.sync="activeTab" :tabs="tabData">
      <component :is="activeTab.component"></component>
    </TabContainer>
  </div>
</template>

<script>
import UserInfo from '../components/UserInfo.vue';
import UserProfiles from '../components/UserProfiles.vue';
import Other from '../components/Other.vue';
import TabContainer from '../components/TabContainer.vue';
// @ is an alias to /src

export default {
  name: 'Home',
  components: {
    TabContainer,
    UserInfo,
    UserProfiles,
    Other,
  },
  data() {
    return {
      tabData: Array,
      activeTab: Object,
    };
  },
  created() {
    this.tabData = [
      {
        displayTitle: 'Info',
        component: UserInfo,
      },
      {
        displayTitle: 'Profiles',
        component: UserProfiles,
      },
      {
        displayTitle: 'Other',
        component: Other,
      },
    ];
    [this.activeTab] = this.tabData;
  },
  methods: {
    getLastSection() {
      return this.tabData.length;
    },
    nextSection() {
      if (this.tabData.indexOf(this.activeTab) < this.getLastSection() - 1) {
        this.activeTab = this.tabData[(this.tabData.indexOf(this.activeTab)) + 1];
      }
    },
    previousSection() {
      if (this.tabData.indexOf(this.activeTab) > 0) {
        this.activeTab = this.tabData[(this.tabData.indexOf(this.activeTab)) - 1];
      }
    },

  },
  mounted() {
    window.addEventListener('keyup', (event) => {
      if (event.key === 'ArrowRight') {
        this.nextSection();
      } else if (event.key === 'ArrowLeft') {
        this.previousSection();
      }
    });
  },
};
</script>

<style lang="scss" scoped>
.container{
  padding: 5px;
}
</style>
