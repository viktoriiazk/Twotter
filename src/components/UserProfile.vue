<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{ user.username }}</h1>
      <div class="user-profile_admin-badge" v-if="user.isAdmin">Admin</div>
      <div class="user-profile_user-badge" v-else>Not Admin</div>
      <div class="user-profile__follower-count">
        <strong>Followers: </strong> {{ followers }}
      </div>
<form class="user-profile__create-twoot" @submit.prevent="createNewTwoot">
  <label for="newTwoot">
    <strong>New Twoot</strong>
  </label>
  <textarea id="newTwoot" rows="4" v-model="newTwootContent"/>


  <div class="user-profile_create-twoot-type">
    <label for="newTwootType"> <strong>Type:</strong></label>
    <select id="newTwootType" v-model="selectedTwootType" >
 <option :value="option.value" v-for="(option, index) in twootTypes" :key="index">
      {{ option.name }}
    </option>
    </select>
  </div>

  <button>
    Twoot!
  </button>
</form>

    </div>
    <div class="user-profile__twoots-wrapper">
        <TwootItem 
        v-for="twoot in user.twoots" 
        :key="twoot.id" 
        :username="user.username" 
        :twoot="twoot" 
        @favourite="toggleFavourite" />
    </div>
  </div>
</template>

<script>
import TwootItem from "./TwootItem";
export default {
  name: "UserProfile",
  components: { TwootItem },
  data() {
    return {
      newTwootContent: '',
      selectedTwootType: 'instant',
      twootTypes: [
        { value: 'draft', name: 'Draft'},
        { value: 'instant', name: 'Instant Twoot'}
      ],
      followers: 0,
      user: {
        id: 1,
        username: "_ViktoriiaZakorchemna",
        firstName: "Viktoriia",
        lastName: "Zakorchemna",
        email: "viktoriia.zakorchemna@gmail.com",
        isAdmin: false,
        twoots: [
          {
            id: 1,
            content: "twooter is Amazing!",
          },
          {
            id: 2,
            content: "Don't forget to subscriber to The Earth is Square!",
          },
        ],
      },
    };
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount) {
        console.log(`${this.user.userName} has gained a follower!`);
      }
    },
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    },
  },
  methods: {
    followUser() {
     this.followers++;
    },
    toggleFavourite(id) {
      console.log(`Favourited Twoot ${id}`);
    },
    createNewTwoot() {
      if (this.newTwootContent && this.selectedTwootType !== 'draft') {
        this.user.twoots.unshift (
           { id: this.user.twoots.length + 1,
           content: this.newTwootContent})
      }
    }
  },
  mounted() {
    this.followUser();
  },
};
</script>

<style>
.user-profile {
  display: flex;
  justify-content: space-between;
  margin: 20px;
      width: 80vw;
  border: 1px solid #abb2ab;
  border-radius: 5px;
  background-color: #d0d5d0;
  padding: 10px;
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
.user-profile__twoots-wrapper {
  max-width: 700px;
  width: 100%;
}
.user-profile__follower-count {
  text-align-last: start;
}
form {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  margin-top: 10px;
}
textarea {
  width: 300px;
  border: 1px solid #abb2ab;
  border-radius: 5px;
}

</style>