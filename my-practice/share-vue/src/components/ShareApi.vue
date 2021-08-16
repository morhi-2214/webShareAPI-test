<template>
  <!-- SPAにおけるShareAPIの挙動調査のためのモックです -->
  <div>
    <h1>ShareAPI テスト</h1>
    <button v-if="isSupportShare" type="button" @click="share">共有する</button>
    <button v-if="!isSupportShare" type="button">
      ブラウザが対応していません
    </button>
  </div>
</template>

<script>
export default {
  computed: {
    isSupportShare() {
      if (process.client) {
        return !!navigator.share;
      } else {
        return false;
      }
    },
  },
  methods: {
    async share() {
      try {
        await navigator.share({
          title: "Share title",
          text: "Share content",
          url: "https://demo.jp/demo",
        });
        console.log("Successful share");
      } catch (err) {
        console.log("Error sharing", err);
      }
    },
  },
  mounted: {},
};
</script>
