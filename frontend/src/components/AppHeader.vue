<script setup lang="ts">
import { ref, computed } from 'vue'
import type { ComputedRef } from 'vue'
import { useUserStore } from '@/stores/user'

const userStore = useUserStore()

interface IMenuItem {
  label: string
  icon: string
  path: string
  show: ComputedRef
}

const items = ref<IMenuItem[]>([
  {
    label: 'Log in',
    icon: 'pi pi-user',
    path: '/auth',
    show: computed((): boolean => !userStore.userId)
  },
  {
    label: 'Wall',
    icon: 'pi pi-warehouse',
    path: '/wall',
    show: computed((): boolean => !!userStore.userId)
  },
  {
    label: 'Messages',
    icon: 'pi pi-envelope',
    path: '/messages',
    show: computed((): boolean => !!userStore.userId)
  },
  {
    label: 'Support',
    icon: 'pi pi-info-circle',
    path: '/support',
    show: computed((): boolean => !!userStore.userId)
  }
])
</script>

<template>
  <app-menubar :model="items" class="md:px-20 px-4">
    <template #start>
      <router-link to="/">
        <span class="text-xl mr-3 font-bold tracking-tight text-orange-500 md:text-2xl"
          >Wow-social.com</span
        >
      </router-link>
    </template>
    <template #item="{ item, props }">
      <template v-if="item.show">
        <router-link :to="item.path" class="flex items-center" v-bind="props.action">
          <span :class="item.icon" class="p-menuitem-icon" />
          <span>{{ item.label }}</span>
        </router-link>
      </template>
    </template>
    <template #end>
      <span
        v-if="userStore.userId"
        @click="userStore.userId = ''"
        class="flex items-center cursor-pointer"
      >
        <span class="pi pi-sign-out" />
        <span class=""> Log out</span>
      </span>
    </template>
  </app-menubar>
</template>
