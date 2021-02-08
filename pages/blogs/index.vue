<template>
  <div>
    <!-- ブログ記事一覧を表示 -->
    <div v-for="b in blogs" :key="b.slug">
      <nuxt-link :to="'/blogs/' + b.slug">{{ b.title }} {{ b.date }}</nuxt-link>
    </div>
  </div>
</template>
<script>
export default {
  // asyncDataはコンポーネントをロードする前に毎回呼び出される
  // nuxt/contentモジュールによって、どこからでもthis.$content にアクセスできる
  async asyncData({ $content, params }) {
    // ブログ記事10件を読み込む
    const query = await $content("blogs" || "index").limit(10);
    // fetch メソッドで非同期データの取得
    const blogs = await query.fetch();
    return { blogs };
  },
};
</script>