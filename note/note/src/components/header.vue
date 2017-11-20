<template>
    <header class="header">
      <!-- search -->
      <div class="header__searchbox">
        <input :disabled="$route.path == '/create/'" class="header__searchbox--input" type="text" placeholder="根据标题搜索" v-model="quest"  @keyup="setEngineSearch(quest)">
      </div>

      <!-- buttons -->
      <div class="header__btngroup">
        <button v-link="'/'" class="header__btngroup--new" type="button">主页</button>
        <button v-link="'/create/'" class="header__btngroup--new" type="button">创建</button>
        <button v-if="($route.path == '/create/') || ($route.name == 'edit')" v-link="'/'" class="header__btngroup--save" type="button" @click="addNote($route.params.noteId)">保存</button>
      </div>
    </header>
</template>

<script>
  export default {
    vuex: {
      actions: {
        // Add note
        // ========
        addNote ({ dispatch }, noteId) {
          dispatch('ADD_NOTE', noteId);
        },

        // Set engine
        // ==========
        setEngineSearch ({ dispatch }, engine) {
          dispatch('SET_ENGINE_SEARCH', engine);
        }
      }
    },

    data () {
      return {

      }
    }
  }
</script>

<style>
  $gray_first: #a1f2d5;
  $gray_second: #1cd996;
  $main_color: #67e0b5;

  @define-extend btn {
    border: none;
    border-radius: 4px;
    background-color: white;
  }

  .header {
    display: flex;
    width: 100%;
    height: 100px;
    background-image: linear-gradient(to right, $gray_first 70%, $gray_second, $gray_first 70%);

    /*Search Box*/
    > .header__searchbox {
      width: auto;
      max-width: 300px;
      margin: 26px auto;
      flex-basis: 300px;


      > .header__searchbox--input {
        border: none;
        border-radius: 4px;
        padding: 5px;
        width: 100%;
        height: 30px;

        &:disabled {
          cursor: not-allowed;
        }
      }
    }

    /*Buttons group*/
    > .header__btngroup {
      margin: 26px auto;
      flex-basis: 300px;

      > .header__btngroup--new,
      > .header__btngroup--save {
        @extend btn;
        padding: 15px;
        transition: all .3s ease;
        color: #aaa;

        &:hover {
          color: white;
          background-color: $main_color;
        }
      }

    }
  }
</style>
