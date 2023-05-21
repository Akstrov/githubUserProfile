<template>
  <div class="ui card">
    <div class="image">
      <img :src="avatar" alt="avatar" />
    </div>
    <div class="content">
      <a :href="profileLink" class="header"
        ><slot>{{ name }}</slot></a
      >
      <div class="meta">
        <span class="date">Joined in {{ joiningDate }}</span>
      </div>
      <div class="description">{{ description }}</div>
    </div>
    <div class="extra content">
      <a :href="freindsLink">
        <i class="user icon"></i>
        {{ friends }} Friends
      </a>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  data() {
    return {
      name: '',
      profileLink: '',
      avatar: '',
      joiningDate: '',
      description: '',
      friends: '',
      freindsLink: ''
    }
  },
  props: {
    username: String
  },
  async created() {
    await axios.get('https://api.github.com/users/' + this.username).then((response) => {
      console.log(response.data)
      this.name = response.data.name
      this.profileLink = response.data.html_url
      this.avatar = response.data.avatar_url
      this.joiningDate = response.data.created_at.split('T')[0]
      this.description = response.data.bio
      this.friends = response.data.followers
      this.freindsLink = response.data.followers_url
    })
  }
}
</script>
