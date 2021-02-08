<template>
  <!-- ブログ記事本文を表示 -->
  <article>
    <h1>{{ blogs.title }}</h1>
    <p>{{ blogs.date }}</p>
    <nuxt-content :document="blogs" />
  </article>
</template>
<script>
export default {
  // nuxt/contentモジュールによって、どこからでもthis.$content にアクセスできる
  async asyncData({ $content, params }) {
    // ページフォルダ内に _slug.vue というファイルがある場合、context の params.slug で値にアクセスできる
    // $content('article', params.slug) は /articles/${params.slug} に変換される(記事ごとのURLになる)
    // fetch メソッドで非同期データの取得
    const blogs = await $content("blogs", params.slug || "index").fetch();
    return { blogs };
  },
};
</script>