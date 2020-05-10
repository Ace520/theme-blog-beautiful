<template>
  <div id="base-list-layout" class="content-wrapper content-wrapper-auto">
    <div class="ui-posts" itemscope itemtype="http://schema.org/Blog">
      <article
        v-for="page in pages"
        :key="page.key"
        class="ui-post"
        itemprop="blogPost"
        itemscope
        itemtype="https://schema.org/BlogPosting"
      >
      <div class="ui-post-right" />
        <div class="ui-post-left">
          <meta itemprop="mainEntityOfPage" :content="page.path" />

          <header class="ui-post-title" itemprop="name headline">
            <NavLink :link="page.path">{{ page.title }}</NavLink>
          </header>

          <p class="ui-post-summary" itemprop="description">
            {{ page.frontmatter.summary || page.summary }}
            <!-- <Content :page-key="page.key" slot-key="intro"/>-->
          </p>

          <footer>
            <div
              v-if="page.frontmatter.author"
              class="ui-post-meta ui-post-author"
              itemprop="publisher author"
              itemtype="http://schema.org/Person"
              itemscope
            >
              <NavigationIcon />
              <span itemprop="name">{{ page.frontmatter.author }}</span>
              <span
                v-if="page.frontmatter.location"
                itemprop="address"
              >&nbsp; in {{ page.frontmatter.location }}</span>
            </div>

            <div v-if="page.frontmatter.date" class="ui-post-meta ui-post-date">
              <ClockIcon />
              <time
                pubdate
                itemprop="datePublished"
                :datetime="page.frontmatter.date"
              >{{ resolvePostDate(page.frontmatter.date) }}</time>
            </div>

            <div v-if="page.frontmatter.tags" class="ui-post-meta ui-post-tag" itemprop="keywords">
              <TagIcon />
              <router-link
                v-for="tag in resolvePostTags(page.frontmatter.tags)"
                :key="tag"
                :to="'/tag/' + tag"
              >{{ tag }}</router-link>
            </div>
          </footer>
        </div>

        
      </article>
    </div>

    <component :is="paginationComponent" v-if="$pagination.length > 1 && paginationComponent"></component>
  </div>
</template>

<script>
/* global THEME_BLOG_PAGINATION_COMPONENT */

import Vue from 'vue'
import dayjs from 'dayjs'
import { NavigationIcon, ClockIcon, TagIcon } from 'vue-feather-icons'
import {
  Pagination,
  SimplePagination,
} from '@vuepress/plugin-blog/lib/client/components'

export default {
  components: { NavigationIcon, ClockIcon, TagIcon },

  data() {
    return {
      paginationComponent: null,
    }
  },

  computed: {
    pages() {
      return this.$pagination.pages
    },
  },

  created() {
    this.paginationComponent = this.getPaginationComponent()
  },

  methods: {
    getPaginationComponent() {
      const n = THEME_BLOG_PAGINATION_COMPONENT
      if (n === 'Pagination') {
        return Pagination
      }

      if (n === 'SimplePagination') {
        return SimplePagination
      }

      return Vue.component(n) || Pagination
    },

    resolvePostDate(date) {
      return dayjs(date).format(
        this.$themeConfig.dateFormat || 'ddd MMM DD YYYY'
      )
    },

    resolvePostTags(tags) {
      if (!tags || Array.isArray(tags)) return tags
      return [tags]
    },
  },
}
</script>

<style lang="stylus">
.common-layout {
  .content-wrapper {
    padding-bottom: 80px;
  }
}

.ui-post {
  padding: 1rem;
  border-bottom: 1px solid $borderColor;
  display: flex;

  &:last-child {
    border-bottom: 0px;
    margin-bottom: 0px;
  }
}

.ui-post:hover {
  box-shadow: 0 8px 15px rgba(0, 0, 0, 0.2);
  transition: all 0.5s;
}

.ui-post-left {
  flex: 2;
  display: flex;
  flex-direction: column;
  padding-left: 1rem;
}

.ui-post-right {
  flex: 1;
  width: 20rem;
  height: 13rem;
  background-image: url('http://pic.netbian.com/uploads/allimg/200411/230125-1586617285f2f6.jpg');
  border-radius: 4px;
  box-shadow: 0 8px 15px rgba(0, 0, 0, 0.1);
  background-repeat: no-repeat;
  background-position: 50%;
  background-size: cover;
}

.ui-post-title {
  font-family: PT Serif, Serif;
  font-size: 28px;
  border-bottom: 0;

  a {
    cursor: pointer;
    color: $darkTextColor;
    transition: all 0.2s;
    text-decoration: none;

    &:hover {
      text-decoration: underline;
    }
  }
}

.ui-post-summary {
  font-size: 14px;
  color: rgba($darkTextColor, 0.54);
  font-weight: 200;
  flex: 1;
}

.ui-post-meta {
  display: inline-flex;
  align-items: center;
  font-size: 12px;
  line-height: 12px;

  &:not(:last-child) {
    margin-bottom: 3px;
    margin-right: 20px;
  }

  svg {
    margin-right: 5px;
    width: 14px;
    height: 14px;
  }

  @media (max-width: $MQMobile) {
    display: flex;

    &:not(:last-child) {
      margin-bottom: 10px;
    }
  }
}

.ui-post-author {
  color: rgba($darkTextColor, 0.84);
  font-weight: 400;
}

.ui-post-date {
  color: rgba($darkTextColor, 0.54);
  font-weight: 200;
}

.ui-post-tag {
  color: rgba($darkTextColor, 0.54);
  font-weight: 200;

  a {
    color: inherit;
    font-weight: 200;
    text-decoration: none;
    margin-right: 5px;

    &:hover {
      color: $accentColor;
    }
  }
}

@media (max-width: $MQMobile) {
  .ui-post {
    flex-direction: column;
  }

  .ui-post-left {
    padding-right: 0;
  }

  .ui-post-right {
    flex: none;
    width: 100%;
    height: 50vw;
    margin-bottom: 1rem;
  }

  .ui-post-title {
    font-family: PT Serif, Serif;
    font-size: 28px;
    border-bottom: 0;
  }
}
</style>
