<template>
  <div>
    <h1 class="text-4xl font-semibold m-3">Plain Drafts</h1>

    <main id="app">
      <div id="memo-post">
        <textarea
          class="bg-white shadow-md rounded-l-lg px-8 pt-6 pb-8"
          placeholder="write text here..."
          rows="5"
          cols="100"
          type="text"
          v-model="currentText"
          v-on:keydown.enter.ctrl="push(currentText)"
          v-on:keydown.c.ctrl="clear()"
        ></textarea>
        <button
          id="add"
          class="bg-blue-500 hover:bg-blue-700 text-white font-bold py- px-4 rounded-r-lg"
          v-on:click="push(currentText)"
        >
          <p class="text-xl">Add</p>
          <p class="font-normal">Ctrl + Enter</p>
        </button>
        <button
          id="clear"
          class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-lg"
          v-on:click="clear()"
        >
          <p class="text-xl">Clear All</p>
          <p class="font-normal">Ctrl + C</p>
        </button>
      </div>
      <article>
        <section class="rounded overflow-hidden shadow-lg" v-if="memos.length === 0">No List Items</section>
        <section
          class="rounded shadow-lg px-8 pt-6 pb-8"
          v-for="(p, index) in memos"
          v-bind:key="index"
        >
          <div class="memo">
            <p v-text="p"></p>
          </div>
          <button
            class="bg-white hover:bg-gray-100 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow"
            v-on:click="edit(index)"
          >Edit</button>
          <button
            class="bg-white hover:bg-gray-100 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow ml-2"
            v-on:click="copy(index)"
          >Copy</button>
          <button
            class="bg-gray-400 hover:bg-gray-300 text-black font-semi-bold px-2 border border-gray-400 rounded-full shadow ml-2"
            v-on:click="deleteItem(index)"
          >×</button>
        </section>
      </article>
    </main>
  </div>
</template>

<style scoped>
body {
  margin: 0;
  padding: 0 20vw;
  background-color: #fff;
}

/* 画面幅900px以下の場合に適用 */
@media (max-width: 900px) {
  body {
    padding: 0
  }

  #memo-post {
    position: sticky;
    top: 0;

    display: block !important;

    padding: 1rem;

    background-color: rgba(144, 185, 255, 0.235);
    border-radius: 15px;
  }

  /* ボタンのレイアウトを変更 */
  #clear,
  #add {
    display: block;
    width: 100%;
    border-radius: 0.5rem;
    margin-top: 0.8rem;
    height: 4rem;
  }
  /* ショートカットキーを非表示 */
  #clear p:nth-child(2) {
    display: none;
  }
  #add p:nth-child(2) {
    display: none;
  }
  /* レイアウトの調整 */
  #clear {
    margin-top: 0.5rem;
  }
  textarea {
    width: 100%;
    border-radius: 0.5rem;
    outline: 0px;
  }
  h1{
    font-size: 28px;
  }
}

main {
  background-color: #ffffff;
}
h1 {
  text-align: center;
}

/* メモ投稿エリア */
#memo-post {
  position: sticky;
  top: 0;

  display: flex;
  flex-flow: row nowrap;

  padding: 1rem;

  background-color: rgba(144, 185, 255, 0.235);
  border-radius: 15px;
}

#memo-post input[type="text"] {
  width: 100%;
}

button {
  white-space: nowrap;
  margin: 0.1rem;
}

article {
  display: flex;
  flex-direction: column-reverse;
  width: 100%;
}

/* textareaにfocusした時のborderを非表示に */
textarea {
  outline: 0px;
  width: 100%;
}

/*　メモセクション */
article section {
  margin: 0.5rem;
  padding: 1rem;

  display: flex;
  align-items: center;
  flex-flow: row nowrap;

  border: 1px solid #626dd2;
  border-radius: 0.2rem;

  box-sizing: border-box;
}

.memo {
  width: 100%;
}

/* メモのテキスト */
article section p {
  margin: 0;
  /* 改行コードを反映 */
  white-space: pre-wrap;
}
</style>

<script>
import Vue from 'vue'

let store = []
if (localStorage.getItem('store') !== null) {
  store = JSON.parse(localStorage.getItem('store'))
}
export default Vue.extend({
  name: 'Memos',
  data () {
    return {
      currentText: '',
      memos: store,
    }
  },
  methods: {
    push (memo) {
      if (this.currentText.trim() === '') {
        return
      }
      this.memos.unshift(memo)
      this.currentText = ''
      localStorage.setItem('store', JSON.stringify(this.memos))
    },
    clear () {
      if (this.memos.length !== 0) {
        if (confirm('Clear All Items?')) {
          this.memos = []
          localStorage.removeItem('store')
        }
      }
    },
    deleteItem (index) {
      this.memos.splice(index, 1)
      localStorage.setItem('store', JSON.stringify(this.memos))
    },
    copy (index) {
      const copyText = this.memos[index]
      navigator.clipboard
        .writeText(copyText)
        .then(() => {
          alert('copied to clipboard')
        })
        .catch((e) => {
          console.error(e)
        })
    },
    edit (index) {
      this.currentText = this.memos[index]
      this.deleteItem(index)
    },
  },
})
</script>
