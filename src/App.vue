<template>
  <v-app>
    <v-app-bar app color="secondary" dark>
      <v-toolbar-title>TodoList-Vue</v-toolbar-title>
      <v-spacer />
      <v-btn to="/" text>Accueil</v-btn>
      <v-btn to="/taches" text>Mes Tâches</v-btn>
    </v-app-bar>

    <v-main>
      <router-view />
    </v-main>
  </v-app>
</template>
