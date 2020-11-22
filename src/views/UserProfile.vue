
<template>
  <div class="user-profile">
    <div class="user-profile__sidebar">
      <div class="user-profile__user-panel">
<h1 class="user-profile__username">@{{ state.user.username }}</h1>
      <div class="user-profile_admin-badge" v-if="state.user.isAdmin">Admin</div>
      <div class="user-profile_user-badge" v-else>Not Admin</div>
      <div class="user-profile__follower-count">
        <strong>Followers: </strong> {{ state.followers }}
      </div>
     
    </div>

<CreateTwootPanel @add-twoot="addTwoot"/>
      </div>
      
    <div class="user-profile__twoots-wrapper">
      <TwootItem
        v-for="twoot in state.user.twoots"
        :key="twoot.id"
        :username="state.user.username"
        :twoot="twoot"
        @favourite="toggleFavourite"
      />
    </div>
  </div>
</template>

<script>
import { reactive, computed} from 'vue';
import { useRoute } from 'vue-router';
import { users } from '../assets/users';
import TwootItem from "../components/TwootItem";
import CreateTwootPanel from "../components/CreateTwootPannel";
export default {
  name: "UserProfile",
  components: { CreateTwootPanel, TwootItem },
  setup() {
    const route = useRoute();
    const userId = computed(() => route.params.userId );
    const state = reactive({
  followers: 0,
      user: users[userId.value - 1] || users[0] 
    });

function  addTwoot(twoot) {
      state.user.twoots.unshift({id: state.user.twoots.length + 1, content: twoot});
    }

    return {
      state,
      addTwoot,
      userId
    }
  }


};
</script>

<style lang="scss" scoped>
.user-profile {
  display: flex;
  justify-content: space-between;
  margin: 20px;
  border: 1px solid #abb2ab;
  border-radius: 5px;
  padding: 10px;

  .user-profile__follower-count {
    text-align-last: start;
  }
  .user-profile_admin-badge {
    background-color: #292c86;
    width: max-content;
    color: white;
    border-radius: 5px;
    margin-right: auto;
    padding: 0 10px;
    font-weight: bold;
  }

  .user-profile_user-badge {
    background-color: #e463a5;
    width: max-content;
    color: white;
    border-radius: 5px;
    margin-right: auto;
    padding: 0 10px;
    font-weight: bold;
  }
  .user-profile__create-twoot {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    margin-top: 10px;
    &.--exceeted {
      color: red;
      button {
        background-color: red;
      }
    }
  }
 
  .user-profile__twoots-wrapper {
    max-width: 700px;
    width: 100%;
  }
}
</style>