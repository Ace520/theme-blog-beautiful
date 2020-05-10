<template>
  <div
    id="vuepress-theme-blog__post-layout"
    class="post-layout content-wrapper content-wrapper-auto"
  >
    <article
      class="vuepress-blog-theme-content"
      itemscope
      itemtype="https://schema.org/BlogPosting"
    >
      <header>
        <div class="post-header">
          <h1 class="post-title" itemprop="name headline">{{ $frontmatter.title }}</h1>
          <PostMeta
            :tags="$frontmatter.tags"
            :author="$frontmatter.author"
            :date="$frontmatter.date"
            :location="$frontmatter.location"
          />
        </div>
      </header>
      <Content itemprop="articleBody" />
      <footer>
        <Newsletter v-if="$service.email.enabled" />
        <hr />
        <Comment />
      </footer>
    </article>
    <Toc />
  </div>
</template>

<script>
import Toc from '@theme/components/Toc.vue'
import PostMeta from '@theme/components/PostMeta.vue'
import { Comment } from '@vuepress/plugin-blog/lib/client/components'

export default {
  components: {
    Toc,
    PostMeta,
    Comment,
    Newsletter: () => import('@theme/components/Newsletter.vue'),
  },
}
</script>

<style lang="stylus">
@require '../styles/wrapper.styl';

.post-layout {
  display: flex;
}

@media (max-width: $MQMobile) {
  .post-layout {
    display: block;
  }
}

.vuepress-blog-theme-content {
  @extend $wrapper;
  font-size: 16px;
  letter-spacing: 0px;
  font-family: PT Serif, Serif;
  color: $textColor;
  position: relative;
  padding-top: 0;
  padding-left: 0;

  .post-header {
    background-image: linear-gradient(rgba(0, 0, 0, 0.2), rgba(0, 0, 0, 0.2)), url('http://pic.netbian.com/uploads/allimg/200411/230125-1586617285f2f6.jpg');
    padding: 50px 50px;
    border-radius: 4px;
    box-shadow: 0 8px 15px rgba(0, 0, 0, 0.4);
    background-repeat: no-repeat;
    background-position: 50%;
    background-size: cover;
    color: #ffffff;

    .post-title {
      padding-top: 50px;
      margin-top: 0;
    }
  }
}

@media (max-width: $MQMobile) {
  .vuepress-blog-theme-content {
    padding-top: 0;
  }

  .post-title {
    margin-top: 0;
  }
}
</style>
