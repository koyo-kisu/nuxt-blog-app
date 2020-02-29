<template>
  <section class="container">
    <div>
      <h3>Nuxt.jsのタグが付けられた投稿一覧</h3>
      <ul>
        <li v-for="item in items" :key="item.id" class="post-list">
          <h4>
            <span>{{ item.title }}</span>
            <small>ユーザーID：
              <nuxt-link :to="`/users/${item.user.id}`">
                {{ item.user.id }}
              </nuxt-link>
            </small>
          </h4>
          <div>{{ item.body.slice(0, 130) }}...</div>
          <div>コメント：　{{ item.comments_count }}件</div>
          <div>いいね：　{{ item.likes_count }}いいね</div>
          <div>ハッシュタグ：　{{ item.tags[0].name }}</div>
          <div>投稿日：　{{ item.created_at }}</div>
          <p><a :href="item.url">{{ item.url }}</a></p>
        </li>
      </ul>
    </div>
  </section>
</template>

<script>
import { mapGetters } from 'vuex';

export default {
  async asyncData({ store }) {
    if (store.getters['items'].length) {
      return;
    }
    await store.dispatch('fetchItems');
  },
  computed: {
    ...mapGetters(['items'])
  }
};
</script>

<style scoped>
.container {
  min-height: 100vh;
  padding: 16px;
}

h3 {
  margin: 16px 0;
  padding: 8px 0;
  border-bottom: 1px solid #ee5e5e;
}

.post-list {
  margin-top: 30px;
}
</style>