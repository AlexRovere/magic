<template>
  <q-layout view="hHh lpR fFf">


    <q-header class="bg-white q-pa-md">
      <q-toolbar class="bg-white">
        <q-toolbar-title class="cursor-pointer" @click="$router.push('/')">
          <img src="~assets/img/logo-digidrive.webp">
        </q-toolbar-title>
        <q-space />
        <nav class="row items-center" style="gap: 16px">
          <NuxtLink @click="$router.push('/')">
            Accueil
          </NuxtLink>
          <NuxtLink @click="$router.push('game')">
            Jeux
          </NuxtLink>
          <NuxtLink @click="$router.push('about')">
            A propos
          </NuxtLink>
          <NuxtLink @click="$router.push('help')">
            Aide
          </NuxtLink>
          <NuxtLink @click="$router.push('contact')">
            Contact
          </NuxtLink>
          <NuxtLink to="/posts/3">
            post3
          </NuxtLink>
          <NuxtLink v-if="mainStore.user" to="/logged/magic">
            Magic
          </NuxtLink>
          <NuxtLink v-if="!mainStore.user" to="/login">
            Se connecter
          </NuxtLink>
          <NuxtLink v-else @click="logout">
            Déconnexion
          </NuxtLink>
        </nav>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <q-page padding class="column">
        <NuxtPage class="col column" />
      </q-page>
    </q-page-container>

  </q-layout>
</template>
<script setup>
import '~/assets/styles.css'
import { useMainStore } from '~/stores/main.js'
import { useRouter } from 'vue-router'
const $router = useRouter()
const mainStore = useMainStore()




onMounted(async () => {
  mainStore.user = null
  try {
    const user = await account.get()
    mainStore.user = user
  } catch (e) {
    console.error(e)
  }

})

const logout = async () => {
  await account.deleteSessions()
  mainStore.user = null
  $router.push({ name: 'index' })
}

</script>

<style scoped>
a {
  font-size: 20px;
  cursor: pointer;
}

a:hover {
  color: var(--q-primary)
}
</style>