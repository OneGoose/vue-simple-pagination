# vue-simple-pagination
> A simple pagination component with Vue.js

# Demo
http://xujianzhen.com/vue-simple-pagination/
# Requirements
Vue.js (^2.0)
# Install
npm install vue-simple-pagination --save
# Usage
```
<template>
  <Pagination 
   :total-page = "totalPage"
   :each-page = "eachPage"
   :current = "current">
  </Pagination>
</template>

<script>
import Pagination from 'vue-simple-pagination'

export default {
  data () {
    return {
      totalPage: 300,
      current: 4,
      eachPage: 2
    }
  },

  components: {
    Pagination
  }
}
</script>
```
# Props
Name | Default value | Description
---|:---:|---
`totalPage` | `10` | The Total pages of pagination.
`current` | `1` | The Current page of pagination.
`eachPage` | `2` | each side page number of pagination.

# License

[The MIT License](LICENSE)
