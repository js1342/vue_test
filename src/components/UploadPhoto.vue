<template>
  <v-container>
    <h1>파일 업로더</h1>
    <input id="file-selector" ref="file" type="file"
    @change="handleFileUpload()">
    <v-btn @click="upload()" color="primary">업로드</v-btn>
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
      IdentityPoolId: 'us-east-1:5d8864f0-e6ef-47ac-8072-82b45e5d5627'
    }
  },


  methods: {
    handleFileUpload() {
      this.file = this.$refs.file.files[0]
      console.log(this.file, "파일이 선택 되었습니다")
    },
    upload() {
      AWS.config.update({
        region: 'us-east-1',
        credentials: new AWS.CognitoIdentityCredentials({
          IdentityPoolId: 'us-east-1:5d8864f0-e6ef-47ac-8072-82b45e5d5627'
        })
      });

      const s3 = new AWS.S3({
        apiVersion: '2006-03-01',
        params: {
          Bucket: 'clothes-photo'
        }
      })

      let photoKey = this.file.name
      s3.upload({
        Key: photoKey,
        Body: this.file,
        ACL: 'public-read'
      }, (err, data) => {
        if(err) {
          console.log(err)
          return alert('There was an error: ', err.message);
        }
        alert('Successfully uploaded photo.');
        console.log(data)
      })
    },
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
