<template>
  <div>
    <AppHeader :username="user.username" v-if="user.isAdmin" />
    <div class="wrapper-main">
      <div class="user-profile-container">
        <div class="user-username">
          <h1>{{ user.username }}</h1>
          <div class="user-admin-badge" v-if="user.isAdmin">
            Admin
          </div>
        </div>
        <div class="user-follower">
          <p>Followers: {{ followers }}</p>
        </div>
        <button type="button" @click="followUser" class="btn-follow">
          Follow
        </button>
        <div class="AddTweet">
          <form
            class="user-profile-add-tweet"
            @submit.prevent="createNewTweet"
            :class="{ '--exceeded': newTweetCharacterCount > 180 }"
          >
            <label for="tweet"
              ><strong>Add Tweet</strong>({{
                newTweetCharacterCount
              }}/180)</label
            >
            <textarea
              name=""
              id="tweet-text"
              cols="24"
              rows="4"
              v-model="newTweetType"
            ></textarea>
            <div class="user-profile-add-tweet-option">
              <div>
                <label for="newTweetType" class="type"
                  ><strong>Type:</strong></label
                >
                <select id="newTweetType" v-model="selectedTweetType">
                  <option
                    :value="option.value"
                    v-for="(option, index) in tweetTypes"
                    :key="index"
                  >
                    {{ option.name }}
                  </option>
                </select>
              </div>
              <div>
                <button>Tweet</button>
              </div>
            </div>
          </form>
        </div>
      </div>
      <div class="tweet-section">
        <TweetItem
          v-for="tweet in user.tweets"
          :key="tweet.id"
          :username="user.username"
          :tweet="tweet"
          @favourite="toggleFavourite"
        />
      </div>
    </div>
  </div>
</template>

<script>
import TweetItem from './TweetItem'
import AppHeader from './AppHeader'
export default {
  name: 'UserLogin',
  components: {
    TweetItem,
    AppHeader,
  },
  data() {
    return {
      newTweetType: '',
      selectedTweetType: 'instant',
      tweetTypes: [
        { value: 'draft', name: 'Draft' },
        { value: 'instant', name: 'Instant Tweets' },
      ],
      followers: 0,
      user: {
        id: 1,
        username: '@_kumarmx',
        fname: 'Mukesh',
        lname: 'Sangal',
        email: 'mukesh.s@gai.co.in',
        isAdmin: true,
        tweets: [
          { id: 1, content: 'Nice Twitter Tweets' },
          { id: 2, content: 'This is the Whole Bunch Tweets' },
        ],
      },
    }
  },
  watch: {
    followers(newFlowerCount, oldflowerCount) {
      if (oldflowerCount < newFlowerCount) {
        console.log(`${this.user.username} gained a flower!`)
      }
    },
  },
  computed: {
    fullName() {
      return `${this.user.fname} ${this.user.lname}`
    },
    newTweetCharacterCount() {
      return this.newTweetType.length
    },
  },
  methods: {
    followUser() {
      this.followers++
    },
    toggleFavourite(id) {
      console.log(`Favourite Tweet ${id}`)
    },
    createNewTweet() {
      if (
        this.newTweetType &&
        this.selectedTweetType !== this.tweets[1].content
      ) {
        this.user.tweets.unshift({
          id: this.user.tweets.length + 1,
          content: this.newTweetType,
        })
      }
      this.newTweetType = ''
    },
  },
  mount() {
    this.followUser()
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.wrapper-main {
  display: flex;
  width: 95%;
  margin: 50px auto;
}
.user-profile-container {
  display: flex;
  flex-direction: column;
  flex: 1;
  padding: 50px;
  align-items: center;
  background: #e0dddd;
}
button {
  color: #fff;
  background: purple;
  font-size: 16px;
  padding: 10px;
  border: navajowhite;
  border-radius: 5px;
  width: 100%;
  margin: 10px auto;
}
.btn-follow {
  color: #fff;
  background: purple;
  font-size: 16px;
  padding: 10px;
  border: navajowhite;
  border-radius: 5px;
  width: 25%;
  margin: 10px auto;
}
p {
  font-size: 18px;
  color: green;
  font-weight: 900;
}
h1 {
  color: #1e7566;
}
.user-admin-badge {
  color: red;
  background: #fff;
  border-radius: 5px;
}
.user-admin-badge {
  color: red;
  background: #fff;
  border-radius: 5px;
  padding: 9px;
  width: 30%;
  margin: auto;
}
.tweet-section {
  flex: 1;
  text-align: left;
  margin-left: 25px;
}
form.user-profile-add-tweet {
  display: flex;
  margin-top: 10px;
  justify-content: space-between;
}
label {
  margin-bottom: 5px;
}
.user-profile-add-tweet {
  display: flex;
  flex-direction: column;
  margin-top: 10px;
}
.AddTweet {
  width: 50%;
}
.--exceeded {
  color: red;
  border-color: red;
}
.user-profile-add-tweet-option {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.type {
  margin-right: 5px;
}
</style>
