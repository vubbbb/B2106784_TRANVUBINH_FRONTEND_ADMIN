<template>
    <q-layout view="hHh lpR fFf">
  
      <q-header elevated class="bg-primary text-white" height-hint="200">
        <q-toolbar>
          <q-toolbar-title>
            <q-avatar>
              <img src="https://cdn.quasar.dev/logo-v2/svg/logo-mono-white.svg">
            </q-avatar>
            Title
          </q-toolbar-title>
  
          <q-btn dense flat round icon="menu" @click="toggleRightDrawer" />
        </q-toolbar>
  
        <q-tabs align="left">
          <q-route-tab to="/inventory/books" label="Inventory" />
          <q-route-tab to="/customers" label="Customers" />
          <q-route-tab to="/page3" label="Page Three" />
        </q-tabs>
      </q-header>
  
      <q-drawer show-if-above v-model="rightDrawerOpen" side="right" bordered>
        sahdgahsd
      </q-drawer>
  
      <q-page-container>
        <router-view />
      </q-page-container>
  
    </q-layout>
  </template>
  
  <script>
  import { ref } from 'vue'
  
  export default {
    setup () {
      const rightDrawerOpen = ref(false)
  
      return {
        rightDrawerOpen,
        toggleRightDrawer () {
          rightDrawerOpen.value = !rightDrawerOpen.value
        }
      }
    }
  }
  </script>