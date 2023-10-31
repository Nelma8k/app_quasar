<template>
  <q-layout view="lHh Lpr lFf">
    <q-header>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          @click="leftDrawerOpen = !leftDrawerOpen"
          icon="menu"
          aria-label="Menu"

        />

      </q-toolbar>
      <div class="q-px-lg q-pt-xl q-mb-md">
        <div class="text-h3">Tarefas</div>
        <div class="text-subtitle">{{ todaysDate }}</div>
      </div>
      <q-img src="src/assets/tree.jpg" class="header-image absolute-top"/>


    </q-header>

    <q-drawer
        v-model="leftDrawerOpen"
        show-if-above
        :width="250"
        :breakpoint="600"
      >
        <q-scroll-area style="height: calc(100% - 192px); margin-top: 192px; border-right: 1px solid #ddd">
          <q-list padding>
            <q-item
             to="/"
             exact
            clickable v-ripple>
              <q-item-section avatar>
                <q-icon name="list" />
              </q-item-section>

              <q-item-section>
                Tarefas
              </q-item-section>
            </q-item>

            <q-item
              to="/help"
              exact
            clickable v-ripple>
              <q-item-section avatar>
                <q-icon name="help" />
              </q-item-section>

              <q-item-section>
                Ajuda
              </q-item-section>
            </q-item>

            </q-list>
        </q-scroll-area>

        <q-img class="absolute-top" src="src/assets/tree.jpg" style="height: 185px">
          <div class="absolute-bottom bg-transparent">
            <q-avatar size="56px" class="q-mb-sm">
              <img src="https:\/\/0.gravatar.com\/avatar\/c2ef6afd9f1da85295295afd1435ca33">
            </q-avatar>
            <div class="text-weight-bold">Nelma Binguane</div>
            <div>@rstoenescu</div>
          </div>
        </q-img>
      </q-drawer>


    <q-page-container>
      <Keep-Alive>
        <router-view />
      </Keep-Alive>

    </q-page-container>
  </q-layout>
</template>

<script>
import { date } from 'quasar'

export default{
  name: 'MainLayout',

  data () {
    return {
      leftDrawerOpen: false,
    };
  },
  computed: {
    todaysDate() {
      const timeStamp = Date.now();
     return date.formatDate(timeStamp, 'dddd D MMMM'). slice(0, 19);
    }
  },

};
</script>


<style lang="scss">
.header-image{
  height: 100%;
  z-index: -2;
  opacity: 0.9;
  filter: grayscale(5%);
}
</style>
