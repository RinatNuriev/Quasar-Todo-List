<template>
  <q-layout view="lHh lpR lff">

    <q-header elevated class="bg-teal-5 text-white">
      <q-toolbar class="justify-between q-pt-sm q-pb-sm q-pl-xl q-pr-xl">
        <q-btn dense flat round icon="menu" @click="toggleLeftDrawer" />

        <div class="text-h3">My Todo List</div>
        <div class="text-subtitle">{{ dateNow }}</div>

      </q-toolbar>

    </q-header>

    <q-drawer v-model="leftDrawerOpen" show-if-above :width="250" :breakpoint="600">
      <q-scroll-area style="height: calc(100% - 150px); margin-top: 150px; border-right: 1px solid #ddd">
        <q-list padding>

          <div class="q-pa-md q-gutter-sm column">
            <q-btn color="secondary" icon="list" exact label="Todo" to="/" />
            <q-btn color="secondary" icon="help" label="Help" to="help" />
            <q-btn color="secondary" icon="link" label="About" to="about" />
            <q-btn color="secondary" icon="contacts" label="Contacts" to="contacts" />            
          </div>

        </q-list>
      </q-scroll-area>

      <q-img class="absolute-top" src="../assets/photo1675239342.jpeg" style="height: 150px">
        <div class="absolute-bottom bg-transparent">
          <div class="text-weight-bold text-right">Rinat Nuriev</div>
        </div>
      </q-img>
    </q-drawer>

    <q-page-container>
      <keep-alive>
        <router-view />
      </keep-alive>
    </q-page-container>

  </q-layout>
</template>

<script>
import { computed, ref } from 'vue'
import { date } from 'quasar'


export default {
  setup() {
    const leftDrawerOpen = ref(false)

    const dateNow = computed(() => {
      const timeStamp = Date.now()
      return date.formatDate(timeStamp, 'MMMM D dddd')
    })

    return {
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value
      },
      dateNow
    }
  }
}
</script>

<style lang="sass">

</style>