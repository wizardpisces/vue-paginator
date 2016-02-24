// register the paginator component
<style>
ul,li{
  margin: 0px;
  padding: 0px;
}
.paginator li{
  list-style: none;
  display: inline;
}
.paginator li:first-child>a {
  margin-left: 0px;
}
.paginator a{
  border: 1px solid #ddd;
  text-decoration: none;
  position: relative;
  float: left;
  padding: 6px 12px;
  margin-left: -1px;
  line-height: 1.42857143;
  color: #337ab7;
  cursor: pointer
}
.paginator a:hover{
  background-color: #eee;
}
.paginator .active a{
  color: #fff;
  cursor: default;
  background-color: #337ab7;
  border-color: #337ab7;
}
.paginator i{
  font-style:normal;
  color: #d44950;
  margin: 0px 4px;
  font-size: 12px;
}
</style>

<template>
  <ul class="paginator">
    <li class="first" @click="current=1">
      <a>Fisrt</a>
    </li>
    <li class="prev" :class="!hasPrev()&&'disabled'" @click="prev()">
      <a>Prev</a>
    </li>
    <li v-for="number in pages" track-by='$index' :class="number == current && 'active'" @click="go(number)">
      <a>{{number}}</a>
    </li>
    <li class="next" :class="!hasNext()&&'disabled'" @click="next()">
      <a>Next</a>
    </li>
    <li class="last" @click="current=total">
      <a>Last</a>
    </li>
  </ul>

</template>
<script>

module.exports = {
  replace: true,
  props: {
    total: Number,
    size: Number,
    current: Number
  },
  data: function () {
    return {
      current: this.current || 1,
      total: this.total,
      size: this.size || 7
    }
  },

  computed: {
    // get pages to show
    pages: function () {
      var size = this.size
      var total = this.total
      var current = this.current
      var pages = []
      var min = 1
      var max = total

      if (size > total) {
        size = total
        min = 1
        max = size
      }
      while (max >= min && max - min >= size) {
        if (max - current >= current - min) max--
        else if (max - current <= current - min) min++
      }

      for (var i = min; i <= max; i++) {
        pages.push(i)
      }

      return pages
    }
  },

  methods: {
    next: function () {
      if (this.current < this.total) {
        this.current++
      }
    },

    prev: function () {
      if (this.current > 1) this.current--
    },

    go: function (number) {
      this.current = number
    },

    hasNext: function () {
      if (!this.pages.length) return false

      if (this.current >= this.total) return false
      return true
    },

    hasPrev: function () {
      if (!this.pages.length) return false
      if (this.current <= 1) return false
      return true
    }
  }
}

</script>
