<template>
  <div class="cart">
    <Notification
      v-if="error"
      v-on:close="error = false"
      :type="errorType"
      :message="errorMessage"
    />
    <form v-on:submit.prevent="add">
      <div class="field">
        <label class="label">Name</label>
        <div class="control">
          <input
            class="input"
            type="text"
            v-model="name"
            placeholder="Petras"
          />
        </div>
      </div>

      <div class="field">
        <label class="label">Surname</label>
        <div class="control">
          <input
            class="input"
            v-model="surname"
            type="text"
            placeholder="Slekys"
          />
        </div>
      </div>

      <div class="field">
        <div class="control">
          <button
            class="button is-primary"
            :class="loading && 'is-loading'"
            type="submit"
          >
            Add
          </button>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
import Notification from "../components/Notification";

export default {
  name: "Cart",
  components: {
    Notification,
  },
  data() {
    return {
      name: "",
      surname: "",
      loading: "",
      error: false,
      errorMessage: "",
      errorType: "",
    };
  },
  methods: {
    add() {
      this.loading = true;
      fetch("https://bubbly-poised-beak.glitch.me/", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({ name: this.name, surname: this.surname }),
      })
        .then((response) => response.json())
        .then((data) => {
          this.loading = false;
          this.error = true;
          this.errorType = "is-success";
          this.errorMessage = `You have successfully added a name (${data.affectedRows}) to the DB`;
        })
        .catch((error) => {
          this.loading = false;
          this.error = true;
          this.errorType = "is-danger";
          this.errorMessage = error.message;
        });
    },
  },
};
</script>
