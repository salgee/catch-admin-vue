<template>
  <el-switch
    v-model="$attrs.row[field]"
    active-text="启用"
    inactive-text="禁用"
    :active-value="1"
    :inactive-value="2"
    @change="disOrEnable"
  />
</template>

<script>
import { updateRouters } from '@/utils/update-router'

export default {
  name: 'status',
  props: {
    table: {
      value: Object,
      default() {
        return null
      }
    },
    field: {
      value: String,
      default() {
        return null;
      }
    }
  },
  methods: {
    disOrEnable(v) {
      const data = {}
      data[this.field] = v
      this.$http.put('/permissions/show/' + this.$attrs.row.id, data).then(() => {
        this.table.getList()
        updateRouters()
      })
    }
  }
}
</script>
