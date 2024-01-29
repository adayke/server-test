<template>
  <div>
    <b-form-input
      v-model="editableServer.server_name"
      type="text"
      placeholder="Enter server name"
    ></b-form-input>

    <b-form-select v-model="editableServer.server_type" class="mt-3">
      <option value="vds">VDS</option>
      <option value="dedicated">Dedicated</option>
      <option value="hosting">Hosting</option>
    </b-form-select>

    <b-button class="mt-3" variant="primary" @click="updateServer"
      >Edit Server</b-button
    >
  </div>
</template>

<script>
import { defineComponent, ref, watch } from 'vue'
import { BFormInput, BFormSelect, BButton } from 'bootstrap-vue'

export default defineComponent({
  components: {
    BFormInput,
    BFormSelect,
    BButton,
  },
  props: {
    selectedServer: {
      type: Object,
      default: () => {},
    },
  },
  setup(props, { emit }) {
    const editableServer = ref({ ...props.selectedServer })

    watch(
      () => props.selectedServer,
      (newVal) => {
        editableServer.value = { ...newVal }
      },
      { deep: true }
    )

    const updateServer = () => {
      emit('update-server', editableServer.value)
    }

    return { editableServer, updateServer }
  },
})
</script>
