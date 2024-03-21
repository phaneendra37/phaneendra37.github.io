<template>
  <TransitionRoot as="div" :show="isOpen">
    <!-- Start of dialog -->
    <Dialog as="div" class="relative z-10" :class="mainClass">
      <!-- Backdrop transition -->
      <TransitionChild
        v-if="isBackDrop"
        as="template"
        :enter="
          isSlideOver ? 'ease-in-out duration-500' : 'duration-300 ease-out'
        "
        enter-from="opacity-0"
        enter-to="opacity-100"
        :leave="
          isSlideOver ? 'ease-in-out duration-500' : 'duration-200 ease-in'
        "
        leave-from="opacity-100"
        leave-to="opacity-0"
      >
        <div class="fixed inset-0 bg-black bg-opacity-35 transition-opacity" />
      </TransitionChild>

      <!-- Main dialog content -->
      <div
        class="fixed inset-y-0"
        :class="
          isSlideOver
            ? 'pointer-events-none  right-0 flex max-w-full'
            : 'flex min-h-full items-center justify-center inset-x-0'
        "
      >
        <TransitionChild
          as="template"
          :enter="
            isSlideOver
              ? 'transform transition ease-in-out duration-500 sm:duration-700'
              : 'duration-300 ease-out'
          "
          :enter-from="isSlideOver ? 'translate-x-full' : 'opacity-0 scale-95'"
          :enter-to="isSlideOver ? 'translate-x-0' : 'opacity-100 scale-100'"
          :leave="
            isSlideOver
              ? 'transform transition ease-in-out duration-500 sm:duration-700'
              : 'duration-200 ease-in'
          "
          :leave-from="isSlideOver ? 'translate-x-0' : 'opacity-100 scale-100'"
          :leave-to="isSlideOver ? 'translate-x-full' : 'opacity-0 scale-95'"
        >
          <DialogPanel
            as="div"
            :class="{
              [size]: true,
              'pointer-events-auto relative w-screen': isSlideOver,
              'transform overflow-hidden shadow-xl transition-all rounded-xl':
                !isSlideOver,
            }"
          >
            <div
              class="flex h-full flex-col overflow-hidden bg-white shadow-xl"
            >
              <!-- Header slot -->
              <template v-if="isHeader">
                <slot name="header">
                  <div
                    class="px-4 py-2.5 bg-slate-950 text-white flex justify-between items-center"
                    :class="headerClass"
                  >
                    <div>
                      <h3
                        v-if="heading"
                        class="!text-sm !font-medium first-letter:capitalize"
                        :class="heading ? 'mb-[3px]' : ''"
                      >
                        {{ heading }}
                      </h3>
                      <p
                        v-if="subHeading"
                        class="text-xs first-letter:capitalize text-white/90"
                      >
                        {{ subHeading }}
                      </p>
                    </div>
                    <span
                      v-if="isHeaderClose"
                      class="material-symbols-outlined hover:scale-105 duration-300 transition-all hover:rotate-90 opacity-80 hover:opacity-100 cursor-pointer"
                      @click="emit('cancel')"
                      >close</span
                    >
                  </div>
                </slot>
              </template>

              <!-- Body slot -->
              <div
                class="relative flex-1 overflow-y-auto bg-slate-50"
                :class="bodyClass ? bodyClass : 'p-4'"
              >
                <slot name="body">
                  <!-- Default body content -->
                  {{ props }}
                </slot>
              </div>

              <!-- Footer slot -->
              <template v-if="isFooter">
                <slot name="footer">
                  <div
                    class="px-5 py-3 gap-x-2 flex justify-end items-center"
                    :class="footerClass"
                  >
                    <!-- FooterBtn slot -->
                    <slot name="footerBtn" />

                    <!-- Cancel button -->
                    <button
                      v-if="isCancelBtn"
                      :class="cancelBtnClass"
                      class="btn-secondary"
                      :disabled="
                        close == closeLabels[1] || close == closeLabels[2]
                      "
                      @click="closeCanvas"
                    >
                      {{ close }}
                    </button>

                    <!-- Save button -->
                    <button
                      v-if="isSaveBtn"
                      :class="saveBtnClass"
                      class="btn-primary flex items-center gap-x-2.5"
                      :disabled="
                        confirm == confirmLabels[1] ||
                        confirm == confirmLabels[2]
                      "
                      @click="saveCanvas"
                    >
                      <span
                        v-if="
                          confirm == confirmLabels[1] ||
                          confirm == confirmLabels[2]
                        "
                        class="animate-spin border-t-2 block w-5 h-5 rounded-full border-t-white border-x-2 border-x-white/40 border-b-2 border-b-white/40"
                      ></span>
                      {{ confirm }}
                    </button>
                  </div>
                </slot>
              </template>
              <!-- End of footer slot -->
            </div>
          </DialogPanel>
        </TransitionChild>
      </div>
    </Dialog>
    <!-- End of dialog -->
  </TransitionRoot>
</template>
<script setup>
import { defineProps, defineEmits } from "vue";
import {
  Dialog,
  TransitionChild,
  TransitionRoot,
  DialogPanel,
} from "@headlessui/vue";

// Define custom events
const emit = defineEmits(["save", "close", "cancel"]);

// Define props
const props = defineProps({
  // Size of the dialog panel
  size: {
    default: "w-[400px]",
    type: String,
  },
  // Flag indicating whether the dialog is open
  isOpen: {
    default: true,
    type: Boolean,
    required: true,
  },
  // Flag indicating whether the dialog slides over content
  isSlideOver: {
    default: true,
    type: Boolean,
  },
  // Flag indicating whether the header section is displayed
  isHeader: {
    default: true,
    type: Boolean,
  },
  // Flag indicating whether the footer section is displayed
  isFooter: {
    default: true,
    type: Boolean,
  },
  // Flag indicating whether the close button in the header is displayed
  isHeaderClose: {
    default: true,
    type: Boolean,
  },
  // Flag indicating whether the save button in the footer is displayed
  isSaveBtn: {
    default: true,
    type: Boolean,
  },
  // Flag indicating whether the cancel button in the footer is displayed
  isCancelBtn: {
    default: true,
    type: Boolean,
  },
  // Flag indicating whether the backdrop is displayed
  isBackDrop: {
    default: true,
    type: Boolean,
  },
  // CSS class for the main dialog container
  mainClass: {
    type: String,
    default: "canvas-main",
  },
  // CSS class for the header section
  headerClass: {
    type: String,
    default: "canvas-header",
  },
  // CSS class for the body section
  bodyClass: {
    type: String,
    default: "canvas-body",
  },
  // CSS class for the footer section
  footerClass: {
    type: String,
    default: "canvas-footer",
  },
  // CSS class for the save button
  saveBtnClass: {
    type: String,
    default: "canvas-save-button",
  },
  // CSS class for the cancel button
  cancelBtnClass: {
    type: String,
    default: "canvas-cancel-button",
  },
  // Heading text for the dialog
  heading: {
    type: String,
    default: "Heading",
  },
  // Subheading text for the dialog
  subHeading: {
    type: String,
    default: "SubHeading",
  },
  // Labels for different states of the confirmation action
  confirmLabels: {
    type: Array,
    default: () => ["Save", "Saving", "Saved"],
  },
  // Labels for different states of the close action
  closeLabels: {
    type: Array,
    default: () => ["Close", "Closing", "Closed"],
  },
  // Current label for the confirmation action
  confirm: {
    type: String,
    default: "Save",
  },
  // Current label for the close action
  close: {
    type: String,
    default: "Close",
  },
});

// Event handler for the cancel action
const closeCanvas = () => {
  emit("cancel");
};

// Event handler for the save action
const saveCanvas = () => {
  emit("save");
};
</script>
