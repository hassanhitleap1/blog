<template>
  <div class="container">
    <div class="row justify-content-center">
      <div class="col-md-8">
        <div class="card">
          <div class="card-header">Example Component</div>
          <div class="card-body" @keydown="form.errors.removeError($event.target.name)">
            <form >
              <div class="form-group">
                <label for="title">title</label>
                <input
                  type="text"
                  class="form-control"
                  id="title"
                  name="title"
                  placeholder="Enter title"
                  v-model="form.title"
                >
                <small
                  id="title"
                  class="form-text  text-danger"
                  v-if="form.errors.has('title')"
                >{{form.errors.get('title')}}.</small>
              </div>
              <div class="form-group">
                <label for="desc">desc</label>
                <input
                  type="text"
                  class="form-control"
                  id="desc"
                  name="desc"
                  placeholder="Enter description"
                  v-model="form.desc"
                >
                <small
                  id="desc"
                  class="form-text  text-danger"
                  v-if="form.errors.has('desc')"
                >{{form.errors.get('desc')}}</small>
              </div>
              <button type="submit" :disabled="form.errors.anyError()" @click.prevent="save" class="btn btn-primary">Save</button>
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
    return this.errors.hasOwnProperty(filed);
  }

  get(filed) {
    return this.errors[filed][0];
  }

  removeError(filed){
    delete this.errors[filed];
  }


  anyError(){
    if(Object.keys(this.errors).length) return true;
    return false;
  }


}

class Form{
  constructor(data) {
    this.data=data;

    for (let key in data) {
      this[key]=data[key]
    }
     this.errors= new Error();
  }
}

export default {
  data() {
    return {
      form:new Form({
     title: "",
      desc: "",
      }),
    
     
    };
  },
  methods: {
    save: function() {
      axios
        .post(window.location.origin + "/blog/public/" + "api/posts", {
          title: this.title,
          desc: this.desc
        }).then(function(response) { 
             this.form.title='';
              this.form.desc='';
               Vue.notify({
                  group: 'message',
                  type: 'warn',
                  title: 'successfuly add',
                  text: 'you are succefully add!'
              });
            
        }).catch(error => {
            this.form.errors.recoredError(error.response.data.errors);
        });
    }
  }
};
</script>
