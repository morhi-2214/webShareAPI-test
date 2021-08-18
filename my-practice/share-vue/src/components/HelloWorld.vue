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
export default {
  data() {
    return {
      isSupportedWebShareAPI: !!navigator.share,
      values: [
        {
          name: "タイトルのみ",
          option: { title: "Title" },
        },
        {
          name: "テキストのみ",
          option: { text: "Text" },
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
        {
          name: "画像ファイル",
          option: { files: ["../assets/gyudon.jpg"] },
        },
        {
          name: "画像ファイルとタイトル",
          option: { title: "Title", files: ["../assets/gyudon.jpg"] },
        },
        {
          name: "画像ファイルとテキスト",
          option: { text: "Text", files: ["../assets/gyudon.jpg"] },
        },
        {
          name: "画像ファイルとURL",
          option: { url: location.href, files: ["../assets/gyudon.jpg"] },
        },
        {
          name: "画像ファイルとタイトルとテキストとURL",
          option: {
            title: "Title",
            text: "Text",
            url: location.href,
            files: ["../assets/gyudon.jpg"],
          },
        },
        {
          name: "テキストとしてタイトルとURLを送ってみる",
          option: {
            text: "ページタイトルページタイトル https://hoge.jp/hoge/fuga/",
          },
        },
      ],
    };
  },
  methods: {
    handleShareClick(option) {
      navigator
        .share(option)
        .then((p) => {
          console.log("success!", p);
        })
        .catch((e) => {
          console.log("error!", e);
        });
    },
  },
};
</script>

<style scoped></style>
