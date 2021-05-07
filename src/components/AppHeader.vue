<template>
  <div class="header-main">
    <div class="sitebranding">
      <img :src="link" alt="Admin Image" />
    </div>
    <div class="userLoggedin">
      {{ username }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'AppHeader',
  props: {
    username: {
      type: String,
      required: true,
    },
    isAdmin: Boolean,
  },
  data() {
    return {
      url: 'https://gai.co.in',
      link:
        'https://t3.ftcdn.net/jpg/04/09/08/74/240_F_409087411_cQyTkIWhtTZjhCx3qAXQQHwhBCVpVWpx.jpg',
    }
  },
}
</script>

<style scoped>
.header-main {
  display: flex;
  justify-content: space-between;
  padding: 2rem 3rem;
  align-items: center;
}
img {
  width: 80px;
  height: 80px;
}
.header-main {
  display: flex;
  justify-content: space-between;
  padding: 2rem 3rem;
  align-items: center;
  background: #90afb0;
}
.userLoggedin {
  font-weight: bold;
  font-size: 26px;
}
</style>
