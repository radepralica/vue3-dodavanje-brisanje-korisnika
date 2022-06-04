<template>
  <section>
    <header>
      <h1>Moja Porodica</h1>
    </header>

    <new-friend @add-contact="addContact"></new-friend>

    <friend-contact
      v-for="friend in friends"
      :key="friend.id"
      :id="friend.id"
      :first-name="friend.name"
      :phone-number="friend.phone"
      :email-address="friend.email"
      :is-favorite="friend.isFavorite"
      @toggle-favorite="toggleFavoriteStatus"
      @delete="deleteContact"
    ></friend-contact>
  </section>
</template>

<script>
export default {
  data() {
    return {
      friends: [
        {
          id: 'matej',
          name: 'Matej Pralica',
          phone: '111-111-111-111',
          email: 'matej@gmail.com',
          isFavorite: true,
        },

        {
          id: 'magi',
          name: 'Magdalena Prišić',
          phone: '222-222-222-222',
          email: 'magi@gmail.com',
          isFavorite: true,
        },
        {
          id: 'rade',
          name: 'Rade Pralica',
          phone: '333-333-333-333',
          email: 'rade@gmail.com',
          isFavorite: false,
        },
      ],
    };
  },
  methods: {
    toggleFavoriteStatus(friendId) {
      const identFriend = this.friends.find((friend) => friend.id === friendId);
      identFriend.isFavorite = !identFriend.isFavorite;
    },
    addContact(name, phone, email) {
      const newFriendContact = {
        id: new Date().toISOString(),
        name: name,
        phone: phone,
        email: email,
        isFavorite: false,
      };
      this.friends.push(newFriendContact);
    },
    deleteContact(friendId) {
      this.friends = this.friends.filter((friend) => friend.id !== friendId);
    },
  },
};
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

* {
  box-sizing: border-box;
}

html {
  font-family: 'Jost', sans-serif;
}

body {
  margin: 0;
}

header {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  margin: 3rem auto;
  border-radius: 10px;
  padding: 1rem;
  background-color: deepskyblue;
  color: white;
  text-align: center;
  width: 90%;
  max-width: 40rem;
}

#app ul {
  margin: 0;
  padding: 0;
  list-style: none;
}

#app li {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  margin: 1rem auto;
  border-radius: 10px;
  padding: 1rem;
  text-align: center;
  width: 90%;
  max-width: 40rem;
}

#app h2 {
  font-size: 2rem;
  border-bottom: 4px solid #ccc;
  color: #58004d;
  margin: 0 0 1rem 0;
}

#app button {
  font: inherit;
  cursor: pointer;
  border: 1px solid #fafaf6;
  background-color: deepskyblue;
  color: rgb(242, 215, 7);
  padding: 0.05rem 1rem;
  box-shadow: 1px 1px 2px rgba(0, 0, 0, 0.26);
}

#app button:hover,
#app button:active {
  background-color: #ec3169;
  border-color: #ec3169;
  box-shadow: 1px 1px 4px rgba(0, 0, 0, 0.26);
}
</style>
