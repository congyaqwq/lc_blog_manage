<template>
  <a-sub-menu :key="menuInfo.path" v-bind="$props" v-on="$listeners">
    <span slot="title">
      <span>{{ menuInfo.meta && menuInfo.meta.title }}</span>
    </span>
    <template v-for="item in menuInfo.children">
      <a-menu-item v-if="!item.children" :key="item.path" @click="$router.push({path:item.path,query:$route.query})">
        <span>{{ item.meta && item.meta.title }}</span>
      </a-menu-item>
      <sub-menu v-else :key="item.path" :menu-info="item" />
    </template>
  </a-sub-menu>
</template>

<script>
import { Menu } from "ant-design-vue";

export default {
  name: "SubMenu",
  isSubMenu: true,
  props: {
    ...Menu.SubMenu.props,
    // Cannot overlap with properties within Menu.SubMenu.props
    menuInfo: {
      type: Object,
      default: () => ({})
    }
  }
};
</script>
