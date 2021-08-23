<template>
  <q-layout view="hHh lpR fFf">
    <q-header elevated class="bg-white text-grey-8 q-py-xs" height-hint="58">
      <q-toolbar>
        <q-btn flat no-caps no-wrap rounded class="q-ml-xs" to="/">
          <q-icon name="fab fa-facebook" color="primary" size="lg" />
        </q-btn>

        <q-input
          class="text-black"
          dense
          standout="bg-grey-13"
          v-model="search"
          placeholder="Pesquisar no Facebook"
          rounded
        >
          <template v-slot:prepend>
            <q-icon v-if="search === ''" name="search" />
            <q-icon
              v-else
              name="clear"
              class="cursor-pointer"
              @click="search = ''"
            />
          </template>
        </q-input>
        <q-space />

        <div class="q-gutter-sm row items-center no-wrap">
          <q-btn rounded flat size="sm">
            <q-avatar size="25px">
              <img src="https://cdn.quasar.dev/img/boy-avatar.png" />
            </q-avatar>
            <div class="q-pl-sm text-subtitle1 text-black text-right">
              {{ firstname }}
            </div>
          </q-btn>
          <q-btn round dense flat color="black" icon="apps">
            <q-tooltip>Menu</q-tooltip>
          </q-btn>
          <q-btn
            round
            dense
            flat
            color="black"
            icon="fab fa-facebook-messenger"
          >
            <q-tooltip>Mensseger</q-tooltip>
          </q-btn>
          <q-btn round dense flat color="black" icon="notifications">
            <q-badge color="red" text-color="white" floating> 2 </q-badge>
            <q-tooltip>Notificações</q-tooltip>
          </q-btn>
          <q-btn
            round
            dense
            flat
            color="black"
            icon="fas fa-sort-down"
            align="top"
          >
            <q-tooltip>Conta</q-tooltip>
          </q-btn>
        </div>
      </q-toolbar>
    </q-header>
    <q-drawer show-if-above v-model="leftDrawerOpen" side="left" bordered>
      <q-list>
        <q-item v-ripple clickable>
          <q-item-section avatar>
            <q-avatar size="30px">
              <img src="https://cdn.quasar.dev/img/boy-avatar.png" />
            </q-avatar>
          </q-item-section>

          <q-item-section class=""> Guilherme Teixeira Ais </q-item-section>
        </q-item>

        <q-item v-ripple clickable>
          <q-item-section avatar>
            <q-avatar size="30px" class="q-mr-sm">
              <q-icon name="group" size="md" color="primary"></q-icon>
            </q-avatar>
          </q-item-section>

          <q-item-section> Amigos </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <q-drawer show-if-above v-model="rightDrawerOpen" side="right" bordered>
      <div class="q-pa-md" style="max-width: 350px">
        <q-toolbar class="text-black text-subtitle1">
          <div class="q-mr-md">Contatos</div>
          <q-space />
          <q-input
            class="text-black"
            dense
            standout="bg-grey-13"
            placeholder=""
            rounded
          >
            <template v-slot:append>
              <q-icon v-if="search === ''" name="search" />
              <q-icon
                v-else
                name="clear"
                class="cursor-pointer"
                @click="search = ''"
              />
            </template>
          </q-input>
        </q-toolbar>

        <q-list bordered>
          <q-item
            v-for="contact in contacts"
            :key="contact.id"
            class="q-my-sm"
            clickable
            v-ripple
          >
            <q-item-section avatar>
              <q-avatar color="primary" text-color="white">
                {{ contact.letter }}
              </q-avatar>
            </q-item-section>

            <q-item-section>
              <q-item-label>{{ contact.name }}</q-item-label>
              <q-item-label caption lines="1">{{ contact.email }}</q-item-label>
            </q-item-section>

            <q-item-section side>
              <q-icon name="chat_bubble" color="green" />
            </q-item-section>
          </q-item>

          <q-separator />
          <q-item-label header>Offline</q-item-label>

          <q-item
            v-for="contact in offline"
            :key="contact.id"
            class="q-mb-sm"
            clickable
            v-ripple
          >
            <q-item-section avatar>
              <q-avatar>
                <img :src="`https://cdn.quasar.dev/img/${contact.avatar}`" />
              </q-avatar>
            </q-item-section>

            <q-item-section>
              <q-item-label>{{ contact.name }}</q-item-label>
              <q-item-label caption lines="1">{{ contact.email }}</q-item-label>
            </q-item-section>

            <q-item-section side>
              <q-icon name="chat_bubble" color="grey" />
            </q-item-section>
          </q-item>
        </q-list>
      </div>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { ref, reactive } from "vue";

export default {
  setup() {
    const leftDrawerOpen = ref(false);
    const rightDrawerOpen = ref(false);
    const search = ref("");
    const firstname = ref("Guilherme");
    return {
      search,
      firstname,
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },

      rightDrawerOpen,
      toggleRightDrawer() {
        rightDrawerOpen.value = !rightDrawerOpen.value;
      },
    };
  },
};
</script>
