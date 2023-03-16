<script setup lang="ts">
import {RouterView} from 'vue-router'
import TheNavbar from "@/components/TheNavbar.vue";
import TheFooter from "@/components/TheFooter.vue";</script>

<template>
  <TheNavbar></TheNavbar>
  <div class="main">
    <RouterView/>
  </div>
  <TheFooter></TheFooter>
</template>

<style>

</style>
