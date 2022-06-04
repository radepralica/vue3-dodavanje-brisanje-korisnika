<template>
  <ul>
    <h2>{{ firstName }} {{ isFavorite ? '(Favorite)' : '' }}</h2>
    <button @click="toggleDetails()">{{ captionShow }} Content</button>
    <button @click="toggleFavorite">Toggle Favorite</button>
    <button @click="$emit('delete', id)">Delete Friend</button>
  </ul>

  <li v-if="detailsAreVisible">
    <strong>Phone: {{ phoneNumber }} </strong>
    <br />
    <strong>Email: {{ emailAddress }}</strong>
  </li>
</template>

<script>
export default {
  props: {
    id: {
      type: String,
      required: true,
    },
    firstName: {
      type: String,
      required: true,
    },
    phoneNumber: {
      type: String,
      required: true,
    },
    emailAddress: {
      type: String,
      required: true,
    },
    isFavorite: {
      type: Boolean,
      required: false,
      default: false,
    },
  },
  emits: ['toggle-favorite', 'delete'],

  computed: {
    captionShow() {
      return this.detailsAreVisible ? 'Hide' : 'Show';
    },
  },
  methods: {
    toggleDetails() {
      this.detailsAreVisible = !this.detailsAreVisible;
    },
    toggleFavorite() {
      this.$emit('toggle-favorite', this.id);
    },
  },
  data() {
    return {
      detailsAreVisible: false,
    };
  },
};
</script>

<style>
li {
  list-style-type: none;
}
</style>
