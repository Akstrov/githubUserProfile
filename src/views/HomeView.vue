<script setup>
import GithubProfileCard from '../components/GithubProfileCard.vue'
</script>

<template>
  <main>
    <h1>Search Github User</h1>
    <input
      v-model="username"
      class="input"
      type="text"
      placeholder="Search"
      @keyup.enter="searchUser = username"
      @keydown.enter="searchUser = null"
    />
    <GithubProfileCard v-if="searchUser" :username="searchUser"></GithubProfileCard>
    <GithubProfileCard username="github"></GithubProfileCard>
  </main>
</template>
<script>
export default {
  data() {
    return {
      username: '',
      searchUser: ''
    }
  },
  components: {
    GithubProfileCard
  }
}
</script>
