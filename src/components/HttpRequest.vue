<template>
  <v-container>
    <h1>Http request</h1>
    <div>{{ user.name }}</div>
    <div>{{ user.email }}</div>
    <div>{{ user.phone_number }}</div>
    <div>{{ user.friends }}</div>
  </v-container>
</template>

<script>
// import AWS from 'aws-sdk'
import axios from 'axios'

export default{
  data () {
    return {
      // get 요청으로 받아온 user 변수
      user: null
    }
  },
  created() {
    // 페이지가 로드 될때 유저 정보를 호출하는 http get request
    // get 요청하기
    axios.get(`https://zizqnx33mi.execute-api.us-east-2.amazonaws.com/dev/user/kmj1995kr@gmail.com`)
    .then(response => {
      // JSON responses are automatically parsed.
      // 요청정보가 user 변수에 저장
      this.user = response.data
      console.log(this.user)
    })
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
