<template>
  <v-container>
    <h1>Http request</h1>
  </v-container>
</template>

<script>
// import AWS from 'aws-sdk'
import axios from 'axios'

export default{
  data () {
    return {
      file: null,
      BucketName: 'clothes-photo',
      bucketRegion: 'us-east-1',
      IdentityPoolId: 'us-east-1:5d8864f0-e6ef-47ac-8072-82b45e5d5627'
    }
  },
  created() {
    axios.get(`https://zizqnx33mi.execute-api.us-east-2.amazonaws.com/dev/user/kmj1995kr@gmail.com`)
    .then(response => {
      // JSON responses are automatically parsed.
      this.posts = response.data
      console.log(this.posts)
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
