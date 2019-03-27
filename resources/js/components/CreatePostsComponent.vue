<template>
  <div class="container">
    <div class="row justify-content-center">
      <div class="col-md-8">
        <div class="card">
          <div class="card-header">Example Component</div>

          <div class="card-body">
            <form>
              <div class="form-group">
                <label for="title">title</label>
                <input
                  type="text"
                  class="form-control"
                  id="title"
                  placeholder="Enter title"
                  v-model="title"
                >
                <small
                  id="title"
                  class="form-text text-muted"
                >We'll never share your email with anyone else.</small>
              </div>
              <div class="form-group">
                <label for="desc">desc</label>
                <input
                  type="text"
                  class="form-control"
                  id="desc"
                  placeholder="Enter description"
                  v-model="desc"
                >
                <small
                  id="desc"
                  class="form-text text-muted"
                >We'll never share your email with anyone else.</small>
              </div>
              <button type="submit" @click.prevent="save" class="btn btn-primary">Save</button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  data() {
    return {
      title: "",
      desc: ""
    };
  },
  mounted() {
    console.log("Component mounted.");
  },
  methods: {
    save: function() {
      axios.post(window.location.origin+'/blog/public/'+'api/posts', {
         title: this.title,
         desc: this.desc
        }).then(function (response) {
              console.log(response)
             
            // if(response.data.code==201){
            //     Vue.notify({
            //         group: 'message',
            //         type: 'warn',
            //         title: 'successfuly add',
            //         text: 'you are succefully add!'
            //     })
            // }else{
            //      Vue.notify({
            //         group: 'message',
            //         type: 'warn',
            //         title: 'successfuly add',
            //         text: 'you are succefully add!'
            //     })
            // }
        })
        .catch(function (response) {
            console.log(response)
     
        
         });
    }
  }
};

</script>
