<template>
  <div id="base-list-layout" class="timeline-content content-wrapper content-wrapper-auto">
    <div itemscope itemtype="http://schema.org/Blog">
      <timeline>
        <div v-for="(item, index) in items" :key="index">
          <timeline-title v-if="item.type === 'date'">{{item.title}}</timeline-title>
          <timeline-item v-else>
            <NavLink :link="item.path">{{ item.title }}</NavLink>
          </timeline-item>
        </div>
      </timeline>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import dayjs from 'dayjs'
import { Timeline, TimelineItem, TimelineTitle } from 'vue-cute-timeline'
const theme = 'red'
export default {
  components: {
    Timeline,
    TimelineItem,
    TimelineTitle,
  },
  data() {
    return {
      items: [],
    }
  },

  created() {
    let arr = []
    this.$site.pages.forEach(element => {
      if (element.frontmatter.date) {
        element.index = parseInt(element.frontmatter.date.replace(/-/g, ''))
        arr.push(element)
      }
    })
    function compare(obj1, obj2) {
      let val1 = obj1.index
      let val2 = obj2.index
      if (val1 < val2) {
        return -1
      } else if (val1 > val2) {
        return 1
      } else {
        return 0
      }
    }
    let itemsSort = arr.sort(compare)
    let items = []
    let dateArr = []
    itemsSort.forEach(item => {
      if (dateArr.indexOf(item.frontmatter.date) == -1) {
        items.push({ type: 'date', title: item.frontmatter.date })
        dateArr.push(item.frontmatter.date)
      }
      item.type = 'post'
      items.push(item)
    })
    this.items = items
  },
  methods: {},
}
</script>

<style lang="stylus">
.common-layout {
  .content-wrapper {
    padding-bottom: 80px;
  }
}

.timeline-content {
  max-width: 800px;
}

@media (max-width: $MQMobile) {
}
</style>
