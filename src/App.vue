<template>
  <div id="app">
    <article>
      <p style="color: #ccc">きめ細かいスポンジにあっさりめの生クリーム、メッセージクッキープレート付き♪</p>
      <p style="color: #aaa">サイズは4号～。</p>
      <p style="color: #999">予約は1週間前～。</p>
      <p style="color: #555">お渡しは、たつの市揖保川町のwork gallery koti、もしくは相談で、との事です。</p>
      <p style="color: #333">今年からクリスマスケーキも販売されるそう◎</p>
      <p>こちらは、また別の記事で改めてご紹介させていただきますね。</p>
    </article>
    <div class="voting">
      <div class="voting__text">この記事は面白かったですか？</div>
      <div class="voting__buttons">

        <VoteButton
          v-for="button in buttons"
          :selected="button === user.selectedButton"
          :item="button"
          :key="button.id"
          @button-clicked="castVote(button)"
        />
      </div>
      <span v-if="user.hasVoted" class="voting__thanks">
        ご投票ありがとうございました！
      </span>
      <span class="voting__total">
        {{ voteTotal }}
      </span>
    </div>
  </div>
</template>

<script>
import VoteButton from "./components/VoteButton.vue";

import EmojiSmile from "./assets/grinning-face.png";
import EmojiNeutral from "./assets/neutral-face.png";
import EmojiUnamused from "./assets/unamused-face.png";

export default {
  name: "app",
  components: {
    VoteButton
  },
  data() {
    return {
      buttons: [
        {
          id: "good",
          // emoji: '😀',
          icon: EmojiSmile,
          count: Math.floor(Math.random() * 100),
          cast: false
        },
        {
          id: "average",
          // emoji: '😐',
          icon: EmojiNeutral,
          count: Math.floor(Math.random() * 20),
          cast: false
        },
        {
          id: "bad",
          // emoji: '😒',
          icon: EmojiUnamused,
          count: Math.floor(Math.random() * 10),
          cast: false
        }
      ],
      user: {
        selectedButton: undefined
      }
    };
  },
  computed: {
    voteTotal() {
      return this.buttons.reduce((sum, value) => sum + value.count, 0);
    }
  },
  methods: {
    castVote(clickedButton) {
      const previouslySelectedButton = this.buttons.find(
        button => button === this.user.selectedButton
      );

      if (clickedButton === previouslySelectedButton) return false;

      this.user.selectedButton = clickedButton;
      clickedButton.count += 1;
      previouslySelectedButton.count -= 1;
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top: 1rem;
}

article p {
  margin: 0.2rem;
}

.voting {
  display: flex;
  flex-flow: column nowrap;
  justify-content: center;
  border: 1px solid #ccc;
  padding: 1rem;
  border-radius: 1rem;
  margin: 1rem 0 0;
}

.voting__text {
  display: flex;
  flex-flow: row nowrap;
  justify-content: center;
  margin: 0 0 1rem;
}

.voting__buttons {
  display: flex;
  flex-flow: row nowrap;
  justify-content: center;
}

.voting__total {
  margin-top: 1rem;
  font-weight: bold;
  font-size: 2rem;
  text-align: center;
}

.voting__thanks {
  margin-top: 1rem;
  font-weight: bold;
  font-size: 1.5rem;
  text-align: center;
}
</style>
