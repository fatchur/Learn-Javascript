<template>
    <div class="admin-post-page">
        <section class="update-form">
            <AdminPostForm :post="loadedPost" @submit="onSubmitted"/>
        </section>
    </div>
</template>


<script>
import AdminPostForm from '@/components/Admin/AdminPostForm.vue'
import axios from 'axios'


export default {
  middleware: ['auth'],
  
  components: {
      AdminPostForm
  },

  asyncData(context)  {
      console.log(context.route.params.postId)
      var postId = context.route.params.postId;
      return axios.get( process.env.baseUrl + '/post/' + postId + '.json')
                .then(res => {
                    console.log(res.data)
                    return {loadedPost: res.data}
                })
                .catch(e => context.error(e))
  },

  methods: {
    onSubmitted(postData) {
      axios.put(process.env.baseUrl + '/post/' + this.$route.params.postId + '.json?auth=' + this.$store.state.idToken, postData)
        .then(result => console.log("--> Post Result: " + result))
        .catch(e => console.log(e))
    }
  }

}
</script>


<style scoped>
.update-form {
  width: 90%;
  margin: 20px auto;
}

@media (min-width: 768px) {
  .update-form {
    width: 500px;
  }
}
</style>