<template lang="html">
<ul class="goose-pagination">
  <li
    :class="[current <= 1 ? 'disabled':'', 'goose-pagination-item']"
    @click="handerPageChange(1)">
    &laquo;
  </li>
  <li
    :class="[current <= 1 ? 'disabled':'', 'goose-pagination-item']"
    @click="handerPageChange(current - 1)">
    &nbsp;&lsaquo;
  </li>
  <template v-for="index in showPageNumber">
    <li
      @click = "handerPageChange(index + startShowPage - 1)"
      :class="[allPagesInfo[index + startShowPage - 2]['isSelect'] ? 'active' : '','goose-pagination-item']">
      {{allPagesInfo[index + startShowPage - 2]['content']}}
    </li>
  </template>
  <li
    :class="[current >= total ? 'disabled':'', 'goose-pagination-item']"
    @click="handerPageChange(current + 1)">
    &rsaquo;&nbsp;
  </li>
  <li
    :class="[current >= total ? 'disabled':'', 'goose-pagination-item']"
    @click="handerPageChange(total)">
    &raquo;
  </li>
</ul>
</template>

<script>
export default {
  name: 'Pagination',
  data () {
    return {
      current: this.currentPage,
      isFirst: false,
      isLast: false
    }
  },
  props: {
    eachSideNumber: {
      type: Number,
      default: 2
    },
    total: {
      type: Number,
      require: true,
      default: 10
    },
    currentPage: {
      trpe: Number,
      default: 1
    }
  },
  computed: {
    onEachSide () {
      return this.eachSideNumber * 2 >= this.total ? 2 : this.eachSideNumber
    },
    showPageNumber () {
      return this.onEachSide * 2 + 1
    },
    startShowPage () {
      if (this.current - this.onEachSide <= 1) {
        return 1
      } else if (this.current + this.onEachSide >= this.total) {
        return this.total - (this.onEachSide * 2)
      }
      return this.current - this.onEachSide
    },
    allPagesInfo () {
      return Array(this.total).fill().map((item, index) => {
        item = {
          'index': index,
          'content': index + 1,
          'isSelect': index + 1 === this.current
        }
        return item
      })
    }
  },
  watch: {
  },
  filters () {
  },
  methods: {
    handerPageChange (page) {
      if (page >= this.total) {
        page = this.total
      } else if (page <= 1) {
        page = 1
      }
      this.current = page
      this.$emit('update:currentPage', this.current)
      this.$emit('handerPageChange', this.current)
    }
  }
}
</script>

<style lang="css">
ul,li{
  list-style: none;
}
.goose-pagination {
  overflow: hidden;
  display: inline-flex;
  color:#ccc;
  box-shadow: 0 4px 9.6px 0.4px rgba(214, 219, 223, 0.5);
  border-radius: 1.875rem;
  vertical-align: middle;
  background-color: #fff;
}
.goose-pagination-item{
  cursor: pointer;
  float: left;
  padding: 20px;
  border: none;
  cursor: pointer;
  border-radius: 0;
  background-color: #fff;
}
.active {
  background-color: #d6dbdf;
  color:#000;
}
.disabled {
  /*pointer-events: none;*/
  cursor: not-allowed;
  background-color: rgba(255, 255, 255, 0.6)
}
</style>
