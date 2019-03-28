<template>
  <div class="container">
    <div class="row justify-content-center">
      <div class="col-md-8">
        <div class="card">
          <div class="card-header">Example Component</div>

          <div class="card-body">
            <form @keydown="errors.removeError($event.target.name)">
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
                  class="form-text  text-danger"
                  v-if="errors.has('title')"
                >{{errors.get('title')}}.</small>
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
                  class="form-text  text-danger"
                  v-if="errors.has('desc')"
                >{{errors.get('desc')}}</small>
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
class Error {
  constructor() {
    this.errors = {};
  }

  recoredError(errors) {
    this.errors = errors;
  }

  has(filed) {
    if (this.errors[filed]) {
      return true;
    }
    return false;
  }

  get(filed) {
    return this.errors[filed][0];
  }

  removeError(filed){
    delete this.errors[filed];
  }
}

export default {
  data() {
    return {
      title: "",
      desc: "",
      errors: new Error()
    };
  },
  methods: {
    save: function() {
      axios
        .post(window.location.origin + "/blog/public/" + "api/posts", {
          title: this.title,
          desc: this.desc
        }).then(function(response) { 
             this.title='';
              this.desc='';
               Vue.notify({
                  group: 'message',
                  type: 'warn',
                  title: 'successfuly add',
                  text: 'you are succefully add!'
              });
            
        }).catch(error => {
            this.errors.recoredError(error.response.data.errors);
        });
    }
  }
};
</script>
