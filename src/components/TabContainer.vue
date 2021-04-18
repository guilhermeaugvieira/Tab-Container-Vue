<template>
  <div class="tab-container">
    <ul class="tab-buttons">
      <li
        v-for="(tab, index) in tabs"
        :key="index" :class="{'active': tab === activeTab }"
        @click="$emit('update:activeTab', tab)"
      >
        {{tab.displayTitle}}
      </li>
    </ul>
    <div class="tab-body">
      <transition name="fade">
        <slot></slot>
      </transition>
    </div>

  </div>
</template>

<script>
export default {
  name: 'TabContainer',
  props: {
    activeTab: {
      type: Object,
      required: true,
    },
    tabs: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style lang="scss" scoped>
.fade-enter-active, .fade-leave-active{
  transition: all .4s ease;
}

.fade-enter, .fade-leave-active{
  opacity: 0;
}

.tab-container{
  .tab-buttons{
    list-style: none;
    display: flex;
    gap: 5px;
    padding-bottom: 10px;

    > li {
      padding: 5px;
      border: 1px solid rgba(0,0,0,.2);
      cursor: pointer;

      &:hover{
        background-color: #eee;
      }

      &.active{
        font-weight: bold;
      }
    }
  }
}
</style>
