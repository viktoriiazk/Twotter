<template>
  <div class="twoot-item" @click="favouriteTwoot(twoot.id)">
    <div class="user-profile__twoot">
      <div class="twoot-item__user">@{{ username }}</div>
      <div class="twoot-item__content">
        {{ twoot.content }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TwootItem",
  props: {
    username: {
      type: String,
      required: true,
    },
    twoot: {
      type: Object,
      required: true,
    },
  },
  methods: {
    favouriteTwoot(id) {
      this.$emit("favourite", id);
    },
  },
};
</script>
<style lang="scss" scoped>
.twoot-item {
  background-color: #e4e4e4;
  border-radius: 10px;
  margin: 20px 0;
  cursor: pointer;
  padding: 20px;
  &:hover {
    transform: scale(1.1, 1.1);
  }
}
</style>