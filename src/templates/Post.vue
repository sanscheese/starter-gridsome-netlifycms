<template>
  <Layout :data-title="$page.post.title" :data-subtext="$page.post.teaser">
    <div class="vertical-section-padding">
      <div class="article mx-auto article">
        <div class="meta">
          <p>{{ $page.post.date }}</p> Just a test

          <p>More test</p>
        </div>
        <div>{{$page.post.content}}</div>
      </div>
      <div
        v-for="(component, index) in $page.post.mainContent"
        :key="index"
        class="article article-main"
      >
        {{{component.type}}}
        <!-- {{ component }} -->
        <!-- <Component :is="`NC$`" :content="component"/> -->
        <hr>
      </div>
    </div>
  </Layout>
</template>

<style lang="postcss">
.article {
  width: 90%;
  max-width: 660px;
  margin-left: auto;
  margin-right: auto;
}

.article-main img,
.article-main iframe {
  min-width: 100%;
}

.article-main p,
.article-main ul {
  @apply text-md;
}

.article-main ul li {
  list-style-type: disc;
}
</style>


<script>
export default {
  components: {},
  metaInfo() {
    return {
      title: this.$page.post.title,
      description: this.$page.post.summary,
      meta: [
        { name: "og:url", content: this.$page.post.path, key: "og:url" },
        { name: "og:image", content: this.$page.post.feature, key: "og:image" },
        { name: "og:image:width", content: "1500", key: "og:image:width" },
        { name: "og:image:height", content: "1000", key: "og:image:height" },
        {
          name: "twitter:card",
          content: this.$page.post.summary,
          key: "twitter:card"
        }
      ]
    };
  }
};
</script>

<page-query>
query Post($path: String!) {
  post(path: $path) {
    id
    title
    summary
    slug
    date(format: "YY MMMM DD")
    feature
    timeToRead
    mainContent {
      type
      title
      image
      images {
        image
      }
      body
    }
  }
}
</page-query>
