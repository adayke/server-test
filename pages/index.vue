<template>
  <b-container fluid class="mt-3">
    <b-row>
      <b-col cols="5">
        <ServerList :servers="servers" @select="selectServer" />
      </b-col>

      <b-col cols="7">
        <ServerEditForm
          :selectedServer="selectedServer"
          @update-server="updateServer"
        />
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
import { ref, defineComponent } from 'vue'
import { BContainer, BRow, BCol } from 'bootstrap-vue'
import ServerList from '~/components/ServerList.vue'
import ServerEditForm from '~/components/ServerEditForm.vue'

export default defineComponent({
  components: {
    ServerList,
    ServerEditForm,
    BContainer,
    BRow,
    BCol,
  },
  setup() {
    const servers = ref([
      {
        customer_id: 'user1',
        server_name: 'server7',
        server_type: 'vds',
      },
      {
        customer_id: 'user5',
        server_name: 'server2',
        server_type: 'dedicated',
      },
      {
        customer_id: 'user3',
        server_name: 'server4',
        server_type: 'hosting',
      },
    ])
    const selectedServer = ref({})

    const selectServer = (server) => {
      selectedServer.value = server
    }

    const updateServer = (server) => {
      servers.value.forEach((serv) => {
        if (serv.customer_id === server.customer_id) {
          serv.server_name = server.server_name
          serv.server_type = server.server_type
        }
      })
    }

    return { servers, selectedServer, selectServer, updateServer }
  },
})
</script>
