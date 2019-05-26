<template>
  <div class="home">
    <div class="section">
      <b-field style="width:100%;">
          <b-input 
              style="width:100%;"
              placeholder="文字を入力してください"
              type="is-info"
              v-model="text"
              >
          </b-input>
      </b-field>
      <div class="buttons">
          <b-button type="is-info" @click="speech(text)">まとめて読み上げる</b-button>
          <b-button outlined type="is-warning" @click="text=''">消去する</b-button>
      </div>
    </div>

    <div class="section">
      <div class="columns is-multiline">
        <div v-for="(char, index) in charactersBasic" :key="'c1' + index" class="column is-1">
          <b-button style="width:100%" @click="addToTextAndSpeech(char)">{{char}}</b-button>
        </div>
      </div>

      <div class="columns is-multiline">
        <div v-for="(char, index) in charactersVoicedConsonant" :key="'c2' + index" class="column is-one-fifth">
          <b-button style="width:100%" @click="addToTextAndSpeech(char)">{{char}}</b-button>
        </div>
      </div>

      <div class="columns is-multiline">
        <div v-for="(char, index) in charactersContractedSound" :key="'c3' + index" class="column is-1">
          <b-button style="width:100%" @click="addToTextAndSpeech(char)">{{char}}</b-button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'home',
  data() {
    return {
      charactersBasic: [
        'あ', 'か', 'さ', 'た', 'な', 'は', 'ま', 'や', 'ら', 'わ', 'ん', 'ー',
        'い', 'き', 'し', 'ち', 'に', 'ひ', 'み', 'ー', 'り', 'ー', 'ー', 'ー',
        'う', 'く', 'す', 'つ', 'ぬ', 'ふ', 'む', 'ゆ', 'る', 'ー', 'ー', 'ー',
        'え', 'け', 'せ', 'て', 'ね', 'へ', 'め', 'ー', 'れ', 'ー', 'ー', 'ー',
        'お', 'こ', 'そ', 'と', 'の', 'ほ', 'も', 'よ', 'ろ', 'を', 'ー', 'ー',
      ],

      charactersVoicedConsonant: [
        'が', 'ざ', 'だ', 'ば', 'ぱ',
        'ぎ', 'じ', 'ぢ', 'び', 'ぴ',
        'ぐ', 'ず', 'づ', 'ぶ', 'ぷ',
        'げ', 'ぜ', 'で', 'べ', 'ぺ',
        'ご', 'ぞ', 'ど', 'ぼ', 'ぽ',
      ],

      charactersContractedSound: [
      'きゃ', 'しゃ', 'ちゃ', 'にゃ', 'ひゃ', 'みゃ', 'りゃ', 'ぎゃ', 'じゃ', 'びゃ', 'ぴゃ', 'ー',
      'きゅ', 'しゅ', 'ちゅ', 'にゅ', 'ひゅ', 'みゅ', 'りゅ', 'ぎゅ', 'じゅ', 'びゅ', 'ぴゅ', 'ー',
      'きょ', 'しょ', 'ちょ', 'にょ', 'ひょ', 'みょ', 'りょ', 'ぎょ', 'じょ', 'びょ', 'ぴょ', 'ー',

      ],

      text: ''
    }
  },

  methods:{
    addToTextAndSpeech(char){
      this.addToText(char)
      this.speech(char)
    },

    addToText(char){
      this.text += char
    },

    speech(text){
      // 発言を作成
      const uttr = new SpeechSynthesisUtterance(text)
      // 発言を再生 (発言キューに発言を追加)
      speechSynthesis.speak(uttr)
    },

    checkBrowserIsSupported(){
      if ('speechSynthesis' in window) {
      } else {
        window.alert("このブラウザは音声合成に対応していません。 Google Chromeをお使いください。")
      }
    }
  },

  created(){
    this.checkBrowserIsSupported()
  }


}
</script>
