<template>
  <div>
    <b-list-group>
      <b-list-group-item
        v-for="server in servers"
        :key="server.customer_id"
        @click="selectServer(server)"
        button
      >
        {{ server.server_name }}
      </b-list-group-item>
    </b-list-group>
  </div>
</template>

<script>
import { defineComponent } from 'vue'
import { BListGroup, BListGroupItem } from 'bootstrap-vue'

export default defineComponent({
  components: {
    BListGroup,
    BListGroupItem,
  },
  props: {
    servers: {
      type: Array,
      default: () => [],
    },
  },
  setup(props, { emit }) {
    const selectServer = (server) => {
      emit('select', server)
    }

    return { selectServer }
  },
})
</script>
