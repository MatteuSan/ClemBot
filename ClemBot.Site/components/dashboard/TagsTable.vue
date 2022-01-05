<template>
  <b-table
    paginated
    narrowed
    hoverable
    :per-page="pageSize"
    checkable
    :data="data"
  >
    <b-table-column sortable searchable field="name" label="Name">
      <template #default="props">
        {{ props.row.name }}
      </template>
    </b-table-column>
    <b-table-column sortable searchable field="userName" label="Owner">
      <template #default="props">
        {{ props.row.userName }}
      </template>
    </b-table-column>
    <b-table-column
      class="my-class"
      sortable
      centered
      field="useCount"
      label="Uses"
    >
      <template #default="props">
        <b-tag type="is-dark" size="is-medium">
          {{ props.row.useCount }}
        </b-tag>
      </template>
    </b-table-column>
    <b-table-column class="my-class" field="content" label="Content">
      <template #default="props">
        <div class="box has-background-black has-shadow">
          {{ props.row.content }}
        </div>
      </template>
    </b-table-column>
  </b-table>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  props: {
    data: {
      required: true,
    },
  },
  data() {
    const pageSize = 20
    return {
      pageSize,
    }
  },
})
</script>

<style>
.table thead {
  background-color: #272727;
}
.table thead th {
  color: white;
  font-size: 120%;
}
.pagination-link.is-current {
  color: black;
}
.pagination-previous,
.pagination-next,
.pagination-link {
  color: white;
}

.b-table .table td {
  vertical-align: middle;
}
</style>
