<script setup>
import Modal from './components/Modal.vue';
import { computed, ref, onMounted, useSlots } from 'vue';

const previewModalRef = ref(null);
const listModalRefs = ref(null);
</script>

<template>
  <div class="hstack gap-3">
    <button
      type="button"
      class="btn btn-primary"
      @click="previewModalRef.modal.show()"
    >
      Launch demo modal
    </button>
  </div>

  <Modal ref="previewModalRef" okonly="true">
    <select name="test" id="testSelect">
      <option value="1">1</option>
      <option value="2">2</option>
    </select>
    <button type="button" class="btn btn-primary" @click="modal.value.hide()">
      Launch demo modal
    </button>
  </Modal>

  <div v-for="(n, i) in 4">
    <button
      type="button"
      class="btn btn-danger"
      @click="listModalRefs[i].modal.show()"
    >
      Launch demo modal
    </button>
    <Modal ref="listModalRefs" okonly="true" :key="n">
      {{ n }}
      <select name="test" id="testSelect">
        <option value="1">1</option>
        <option value="2">2</option>
      </select>
      <button type="button" class="btn btn-primary" @click="modal.value.hide()">
        Launch demo modal
      </button>
    </Modal>
  </div>
</template>

<style>
@import 'bootstrap';
</style>
