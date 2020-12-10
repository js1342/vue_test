<template>
  <v-container>
    <h1>파일 리스트</h1>
    <div v-for="file in fileList" :key="file.Key">
      {{file.Key}}
      <img :src="BucketUrl+file.Key">
      <v-btn @click="deleteFile" color="red" flat icon>x</v-btn>
    </div>
  </v-container>
</template>

<script>
import AWS from 'aws-sdk'

export default{
  data () {
    return {
      file: null,
      BucketName: 'clothes-photo',
      bucketRegion: 'us-east-1',
      BucketUrl: "https://clothes-photo.s3.amazonaws.com/",
      IdentityPoolId: 'us-east-1:5d8864f0-e6ef-47ac-8072-82b45e5d5627',
      fileList: []
      
    }
  },

  //웹페이지가 로딩될때 파일을 가져올수 있게 하는것
    created() {
      this.getFiles()
    },
  methods: {
    // 파일 목록 가져오는 함수
    getFiles () {
      // aws configuration
      AWS.config.update({
        region: 'us-east-1',
        credentials: new AWS.CognitoIdentityCredentials({
          IdentityPoolId: 'us-east-1:5d8864f0-e6ef-47ac-8072-82b45e5d5627'
        })
      });

      // s3 버킷설정
      const s3 = new AWS.S3({
        apiVersion: '2006-03-01',
        params: {
          Bucket: 'clothes-photo'
        }
      })

      s3.listObjects({
        Delimiter: '/'
      // arrow function을 쓰면 위에서 썼던 this를 그대로 받아서 쓸수 있음
      }, (err, data) => {
        if (err) {
          return alert('There was an error retrieving objects' + err.message)
        } else {
          this.fileList = data.Contents
          console.log(data.Contents)
        }
      })
    }

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