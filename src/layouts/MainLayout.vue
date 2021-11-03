<template>
  <q-layout view="lHh Lpr lFf q-pa-md">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title> Quasar App </q-toolbar-title>

        <div>Quasar v{{ $q.version }}</div>
      </q-toolbar>
    </q-header>

    <q-page-container class="q-pa-md q-ma-md">
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
  export default {
  name: "MainLayout",
  methods: {
    toggleLeftDrawer() {leftDrawerOpen.value = !leftDrawerOpen.value;},
  },
  data() {
    return {
      locations: [
        {
          country: "Iran",
          city: "Tehran",
        },
      ],
      leftDrawerOpen: false,
    };
  },
};
</script>
