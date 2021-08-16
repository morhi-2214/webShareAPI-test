<template>
  <div class="v-app">
    <div v-if="!isSupportedWebShareAPI">
      <p class="not-support">このブラウザは Web Share API に対応していません</p>
    </div>
    <div class="shares">
      <div class="share" v-for="value in values" :key="value.id">
        <p class="title">{{ value.name }}</p>
        <button
          :disabled="!isSupportedWebShareAPI"
          @click="handleShareClick(value.option)"
        >
          共有する
        </button>
        <hr />
      </div>
    </div>
  </div>
</template>

<script>
// let isSupportedWebShareAPI = !!navigator.share;
export default {
  data() {
    return {
      isSupportedWebShareAPI: true,
      values: [
        {
          name: "タイトルのみ",
          option: { title: "Hello WebShareAPI!" },
        },
        {
          name: "テキストのみ",
          option: { text: "Hello WebShareAPI!(Text)" },
        },
        {
          name: "このサイトのURLのみ",
          option: { url: location.href },
        },
        {
          name: "他のサイトのURLのみ",
          option: { url: "https://www.yahoo.co.jp/" },
        },
        {
          name: "タイトルとテキスト",
          option: { title: "Title", text: "Text" },
        },
        {
          name: "タイトルとURL",
          option: { title: "Title", url: location.href },
        },
        {
          name: "テキストとURL",
          option: { text: "Text", url: location.href },
        },
        {
          name: "タイトルとテキストとURL",
          option: { title: "Title", text: "Text", url: location.href },
        },
      ],
    };
  },
  methods: {
    handleShareClick(option) {
      if (navigator.share) {
        navigator
          .share(option)
          .then((p) => {
            console.log("success!", p);
          })
          .catch((e) => {
            console.log("error!", e);
          });
      }
    },
  },
};
</script>

<style scoped></style>
