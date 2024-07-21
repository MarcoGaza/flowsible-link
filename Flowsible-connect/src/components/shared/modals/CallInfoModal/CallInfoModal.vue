<script setup lang="ts">
import { computed, ref } from "vue";
import { defineProps, defineEmits } from "vue";
import { ICall } from "@src/types";
import CallInfo from "@src/components/shared/modals/CallInfoModal/CallInfo.vue";
import CallMembers from "@src/components/shared/modals/CallInfoModal/CallMembers.vue";
import Button from "@src/components/ui/inputs/Button.vue";
import SlideTransition from "@src/components/ui/transitions/SlideTransition.vue";
import Modal from "@src/components/ui/utils/Modal.vue";

const props = defineProps<{
  call: ICall;
  open: boolean;
  closeModal: () => void;
}>();

const emit = defineEmits(["activePageChange"]);

const activePageName = ref("call-info");
const animation = ref("slide-left");

const ActivePage = computed(() => {
  return activePageName.value === "call-info" ? CallInfo : CallMembers;
});

// (event) move between modal pages
const changeActiveTab = (event: { tabName: string; animationName: string }) => {
  animation.value = event.animationName;
  activePageName.value = event.tabName;
};
</script>

<template>
  <Modal :open="props.open" :closeModal="props.closeModal">
    <template v-slot:content>
      <div
        class="w-[18.75rem] py-6 overflow-x-hidden rounded bg-white dark:bg-gray-800"
      >
        <!--modal content-->
        <SlideTransition :animation="animation">
          <component
            @active-page-change="changeActiveTab"
            :is="ActivePage"
            :call="props.call"
            :close-modal="props.closeModal"
          />
        </SlideTransition>

        <!--Call again button-->
        <div class="px-5">
          <Button color="success" class="w-full py-4">Call again</Button>
        </div>
      </div>
    </template>
  </Modal>
</template>
