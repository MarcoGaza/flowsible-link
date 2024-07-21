<script setup lang="ts">
import { computed } from 'vue';
import useStore from '@src/store/store';

import FadeTransition from '@src/components/ui/transitions/FadeTransition.vue';
import Calls from '@src/components/views/HomeView/Sidebar/Calls/Calls.vue';
import Contacts from '@src/components/views/HomeView/Sidebar/Contacts/Contacts.vue';
import Conversations from '@src/components/views/HomeView/Sidebar/Conversations/Conversations.vue';
import Notifications from '@src/components/views/HomeView/Sidebar/Notifications/Notifications.vue';
import Settings from '@src/components/views/HomeView/Sidebar/Settings/Settings.vue';

const store = useStore();

const ActiveComponent = computed(() => {
    switch (store.activeSidebarComponent) {
        case 'messages':
            return Conversations;
        case 'contacts':
            return Contacts;
        case 'notifications':
            return Notifications;
        case 'phone':
            return Calls;
        case 'settings':
            return Settings;
        default:
            return null;
    }
});
</script>

<template>
    <aside
        class="xs:w-full md:w-[18.125rem] h-full xs:px-5 md:p-0 flex flex-col overflow-visible transition-all duration-500"
    >
        <FadeTransition>
            <component :is="ActiveComponent" class="h-full flex flex-col" />
        </FadeTransition>
    </aside>
</template>
