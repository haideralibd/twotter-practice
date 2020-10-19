<template>
  <div class="user-profile">
    <div class="user-profile_sidebar">
      <div class="user-profile_user-panel">
        <h1 class="user-profile_username">@{{ state.user.username }}</h1>
        <div class="user-profile_admin-badge" v-if="state.user.isAdmin">Admin</div>
        <div class="user-profile_follower_count">
          <strong>Followers: </strong> {{ state.followers }}
        </div>
      </div>

      <CreateTwootPanel @add-twoot="addTwoot" />
    </div>
    <div class="user-profile_toots-wrapper">
      <TwootItem
        v-for="twoot in state.user.twoots"
        :key="twoot.id"
        :username="state.user.username"
        :twoot="twoot"
        @favorite="toggleFavorite"
      />
    </div>
  </div>
</template>
<script>
import {reactive} from 'vue';
import TwootItem from '@/components/TwootItem';
import CreateTwootPanel from '@/components/CreateTwootPanel';

export default {
  name: "UserProfile",
  components: {
    CreateTwootPanel,
    TwootItem
  },

  setup(){
    const state = reactive({
      followers: 0,
      user: {
        id: 1,
        username: "HaiderAliBD",
        firstName: "Haider",
        lastName: "Ali",
        email: "haider4uiu@gmail.com",
        isAdmin: true,
        twoots: [
          { id: 1, content: "Twooter is great!" },
          { id: 2, content: "I like Twooter." },
          { id: 3, content: "Great UI design!" },
        ],
      },

    })

    function addTwoot(twoot){
      state.user.twoots.unshift({id: state.user.twoots.length + 1, content: twoot })
    }

  
  return {
    state,
    addTwoot
  }
  
  }

};
</script>



<style lang="scss" scoped>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  grid-gap: 50px;
  padding: 50px 5%;

  .user-profile_user-panel {
    display: flex;
    flex-direction: column;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #dfe3e8;

    h1 {
      margin: 0;
    }

    .user-profile_admin-badge {
        background: rebeccapurple;
        color: white;
        border-radius: 5px;
        margin-right: auto;
        padding: 0 10px;
        font-weight: bold;
    }

  
    }
}

.user-profile_create_twoot {
    padding-top: 20px;
    display: flex;
    flex-direction: column;
 
    &.--exceeded {
        color: red;
        border-color: red;

      button{
        background-color: red;
        border: none;
        color: white;

      }
    }
 
  }
 



.user-profile_twoots-wrapper {
  display: grid;
  grid-gap: 10px;
}




</style>
