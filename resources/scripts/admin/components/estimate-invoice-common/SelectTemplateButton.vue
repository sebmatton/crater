<template>
  <div>
    <label class="flex text-gray-800 font-medium text-sm mb-2">
      {{ $t('general.select_template') }}
      <span class="text-sm text-red-500"> *</span>
    </label>
    <BaseButton
      type="button"
      class="flex justify-center w-full text-sm lg:w-auto hover:bg-gray-200"
      variant="gray"
      @click="openTemplateModal"
    >
      <template #right="slotProps">
        <BaseIcon name="PencilIcon" :class="slotProps.class" />
      </template>
      {{ store[storeProp].template_name }}
    </BaseButton>
  </div>
</template>

<script setup>
import { useModalStore } from '@/scripts/stores/modal'
import { useI18n } from 'vue-i18n'

const props = defineProps({
  store: {
    type: Object,
    default: null,
  },
  storeProp: {
    type: String,
    default: '',
  },
})

const modalStore = useModalStore()

const { t } = useI18n()

function openTemplateModal() {
  modalStore.openModal({
    title: t('general.choose_template'),
    componentName: 'SelectTemplate',
    data: {
      templates: props.store.templates,
      store: props.store,
      storeProp: props.storeProp,
    },
  })
}
</script>
