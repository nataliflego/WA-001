<template>
  <div class="home">
    <br />
    <br />

    <center>
      <ul>
        <li v-for="nesto in commits" v-bind:key="nesto.sha">
          <router-link :to="'/commit/' + nesto.sha">{{
            nesto.sha
          }}</router-link>
        </li>
      </ul>
    </center>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: "Home",
  data() {
    return {
      commits: [],
    };
  },

  async mounted() {
    let rezultat = await fetch(
      "https://api.github.com/repos/vuejs/vue/commits"
    );

    let podaci = await rezultat.json();

    for (let nesto of podaci) {
      console.log(nesto.sha);
    }

    this.commits = podaci;
  },
};
</script>
