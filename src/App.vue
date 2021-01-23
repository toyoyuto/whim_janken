<template>
  <div id="app">
    <!-- class="result"を追記します。 -->
    <div v-if="isEveryoneSelect"  class="result">
      <div v-for="user in $whim.users" :key="user.id">
        <!-- じゃんけんの画像（rock.pngなど）を出した手に応じて表示します。 -->
        <img
          :src="require('@/assets/' + $whim.state[user.id] + '.png')"
          width="150"
          height="150"
        />
        <h2>{{user.name}}</h2>
      </div>
    </div>
    <div v-else-if="$whim.state[$whim.accessUser.id]">
      <h2>
        {{ $whim.state[$whim.accessUser.id] }}を選択済みです。
      </h2>
    </div>
    <div v-else>
      <h2>
        選択してください！
      </h2>
      <div>
        <img
          src="@/assets/rock.png"
          width="150"
          height="150"
          @click="select('rock')"
        />
        <img
          src="@/assets/scissors.png"
          width="150"
          height="150"
          @click="select('scissors')"
        />
        <img
          src="@/assets/paper.png"
          width="150"
          height="150"
          @click="select('paper')"
        />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  methods: {
    select(hand) {
      // ここに処理を書いていく
      console.log('selectされた！')
      this.$whim.assignState({
        [this.$whim.accessUser.id]: hand
      })
    },
  },
  computed: {
    isEveryoneSelect() {
      let result = true
      for (let i = 0; i < this.$whim.users.length; i++ ) {
        if(!this.$whim.state[this.$whim.users[i].id]){
            result = false
        }  
      }
      return result
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
/* resultクラスに対応するcssを追記します。 */
.result {
  display: flex;
  justify-content: center;
}
</style>