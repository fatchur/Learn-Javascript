<template>
    <div class="admin-new-post-page">
        <section class="new-post-form">
            <AdminPostForm @submit="onSubmitted"/>
        </section>
    </div>
</template>


<script>
import axios from "axios"
import AdminPostForm from '@/components/Admin/AdminPostForm.vue'

export default {

    components: {
        AdminPostForm
    },

    methods: {
      onSubmitted(postData) {
        axios.post(process.env.baseUrl + '/post.json?auth=' + this.$store.state.idToken, postData)
          .then(result => console.log("--> Post Result: " + result))
          .catch(e => console.log(e))
      }
    }
}
</script>

<style scoped>
.new-post-form {
  width: 90%;
  margin: 20px auto;
}

@media (min-width: 768px) {
  .new-post-form {
    width: 500px;
  }
}
</style>