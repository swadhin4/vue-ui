<template>
  <v-simple-table>
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-left">
            Name
          </th>
          <th class="text-left">
            SSO
          </th>
           <th class="text-left">
            Amount
          </th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="item in details"
          :key="item.name"
        >
          <td>{{ item.name }}</td>
          <td>{{ item.sso }}</td>
          <td>{{ item.amount }}</td>
        </tr>
      </tbody>
    </template>
  </v-simple-table>

</template>
<script>
  export default {
    data () {
      return {
        details: [
          {
            name: 'Frozen Yogurt',
            sso: 159,
            amount:12.34
          },
          {
            name: 'Ice cream sandwich',
            sso: 237,
            amount:12.34
          },
          {
            name: 'Eclair',
            sso: 262,
            amount:12.34
          }
        ],
      }
    },
  }
</script>