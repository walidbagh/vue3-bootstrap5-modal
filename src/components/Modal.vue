<template>
  <!-- Modal -->
  <Teleport to="#modals">
    <div
      :id="computedId"
      ref="modalRef"
      class="modal"
      :class="modalClasses"
      role="dialog"
      :aria-labelledby="`${computedId}-label`"
      :aria-describedby="`${computedId}-body`"
      tabindex="-1"
      v-bind="$attrs"
    >
      <div class="modal-dialog" :class="modalDialogClasses">
        <div class="modal-content" :class="contentClass">
          <div
            v-if="!hideHeaderBoolean"
            class="modal-header"
            :class="headerClasses"
          >
            <slot name="header">
              <h1
                :id="`${computedId}-label`"
                class="modal-title fs-5"
                :class="titleClasses"
              >
                <slot name="title">
                  {{ title }}
                </slot>
              </h1>
              <button
                type="button"
                class="btn-close"
                data-bs-dismiss="modal"
                aria-label="Close"
              ></button>
            </slot>
          </div>
          <div
            :id="`${computedId}-body`"
            class="modal-body"
            :class="bodyClasses"
          >
            <slot />
          </div>
          <div
            v-if="!hideFooterBoolean"
            class="modal-footer"
            :class="footerClasses"
          >
            <slot name="footer">
              <slot name="cancel">
                <b-button
                  v-if="!okOnlyBoolean"
                  type="button"
                  class="btn"
                  :class="cancelBtnClass"
                  data-bs-dismiss="modal"
                >
                  {{ cancelTitle }}
                </b-button>
              </slot>
              <slot name="ok">
                <button
                  type="button"
                  class="btn"
                  :class="okBtnClass"
                  :disabled="disableOk"
                >
                  {{ okTitle }}
                </button>
              </slot>
            </slot>
          </div>
        </div>
      </div>
    </div>
  </Teleport>
</template>

<script setup lang="ts">
import { Modal } from 'bootstrap';
import { computed, ref, onMounted, useSlots } from 'vue';

//const show = ref(true);
// declare a ref to hold the element reference
// the name must match template ref value
const modalRef = ref(null);
let modal = ref(null);

const computedId = `__KSID__${Math.random().toString().slice(2, 8)}___KS_`;
const slots = useSlots();

const props = defineProps({
  title: {
    type: String,
    default: 'Title',
  },
  okTitle: {
    type: String,
    default: 'Save',
  },
  cancelTitle: {
    type: String,
    default: 'Close',
  },
  okOnlyBoolean: {
    type: Boolean,
    default: false,
  },
  modalClass: {
    type: String,
    default: 'fade',
    validator: (prop: Type) => ['button', 'submit', 'reset'].includes(prop),
  },
  dialogClass: {
    type: String,
    default: '',
    validator: (prop: Type) => ['button', 'submit', 'reset'].includes(prop),
  },
  bodyClass: {
    type: String,
    default: '',
    validator: (prop: Type) => ['button', 'submit', 'reset'].includes(prop),
  },
  headerClass: {
    type: String,
    default: '',
    validator: (prop: Type) => ['button', 'submit', 'reset'].includes(prop),
  },
  footerClass: {
    type: String,
    default: '',
    validator: (prop: Type) => ['button', 'submit', 'reset'].includes(prop),
  },
  titleClass: {
    type: String,
    default: '',
    validator: (prop: Type) => ['button', 'submit', 'reset'].includes(prop),
  },
  cancelBtnClass: {
    type: String,
    default: 'btn-secondary',
  },
  okBtnClass: {
    type: String,
    default: 'btn-primary',
  },
});

const modalClasses = computed(() => [
  props.modalClass,
  {
    // fade: !noFadeBoolean.value,
    // show: isActive.value,
  },
]);

const modalDialogClasses = computed(() => [
  props.dialogClass,
  {
    // 'modal-fullscreen': props.fullscreen === true,
    // [`modal-fullscreen-${props.fullscreen}-down`]:
    //   typeof props.fullscreen === 'string',
    // [`modal-${props.size}`]: props.size !== undefined,
    // 'modal-dialog-centered': centeredBoolean.value,
    // 'modal-dialog-scrollable': scrollableBoolean.value,
  },
]);
const bodyClasses = computed(() => [
  props.bodyClass,
  {
    // [`bg-${props.bodyBgVariant}`]: props.bodyBgVariant !== undefined,
    // [`text-${props.bodyTextVariant}`]: props.bodyTextVariant !== undefined,
  },
]);
const headerClasses = computed(() => [
  props.headerClass,
  {
    // [`bg-${props.headerBgVariant}`]: props.headerBgVariant !== undefined,
    // [`border-${props.headerBorderVariant}`]:
    //   props.headerBorderVariant !== undefined,
    // [`text-${props.headerTextVariant}`]: props.headerTextVariant !== undefined,
  },
]);
const footerClasses = computed(() => [
  props.footerClass,
  {
    // [`bg-${props.footerBgVariant}`]: props.footerBgVariant !== undefined,
    // [`border-${props.footerBorderVariant}`]:
    //   props.footerBorderVariant !== undefined,
    // [`text-${props.footerTextVariant}`]: props.footerTextVariant !== undefined,
  },
]);
const titleClasses = computed(() => [
  props.titleClass,
  {
    // ['visually-hidden']: titleSrOnlyBoolean.value,
  },
]);

onMounted(() => {
  modal.value = new Modal(modalRef.value, { keyboard: false });
  modalRef.value.addEventListener('show.bs.modal', (event) => {
    // show.value = true;
  });
  modalRef.value.addEventListener('hide.bs.modal', (event) => {
    //show.value = false;
  });
});

defineExpose({
  modal,
});
</script>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
