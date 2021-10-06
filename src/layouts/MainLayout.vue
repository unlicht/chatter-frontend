<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Chats"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title id="title">
          {{titleText}}
        </q-toolbar-title>

        <q-btn
          flat
          dense
          round
          icon="settings"
          aria-label="Settings"
          @click="toggleRightDrawer"
        />
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      :width="260"
      :breakpoint="700"
      elevated
      class="bg-primary text-white"
    >
    <Chats/>
    </q-drawer>
    <q-drawer
      side="right"
      v-model="rightDrawerOpen"
      show-if-above
      bordered
      :width="200"
      elevated
    >
    </q-drawer>
    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import Chats from 'src/components/Chats.vue'
import { defineComponent, ref } from 'vue'

export default defineComponent({
  name: 'MainLayout',

  components: {
    Chats
  },

  setup () {
    const leftDrawerOpen = ref(false)
    const rightDrawerOpen = ref(true)
    const titleText = 'Chatter';

    return {
      leftDrawerOpen,
      rightDrawerOpen,
      titleText,
      toggleLeftDrawer () {
        if(!leftDrawerOpen.value && rightDrawerOpen.value) {
          rightDrawerOpen.value = !rightDrawerOpen.value;
        }

        leftDrawerOpen.value = !leftDrawerOpen.value
      },
      toggleRightDrawer () {
        if(!rightDrawerOpen.value && leftDrawerOpen.value) {
          leftDrawerOpen.value = !leftDrawerOpen.value;
        }

        rightDrawerOpen.value = !rightDrawerOpen.value
      }
    }
  }
})
</script>
