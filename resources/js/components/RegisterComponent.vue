<template>
                   <form @submit.prevent="register(user)">
                      

                        <div class="row mb-3">
                            <label for="name" class="col-md-4 col-form-label text-md-end">Name</label>

                            <div class="col-md-6">
                                <input id="name" type="text" class="form-control @error('name') is-invalid @enderror" name="name" v-model="user.name" required autocomplete="name" autofocus>

                              
                            </div>
                        </div>

                        <div class="row mb-3">
                            <label for="email" class="col-md-4 col-form-label text-md-end">Email Address</label>

                            <div class="col-md-6">
                                <input id="email" type="email"  class="form-control @error('email') is-invalid @enderror" name="email" v-model="user.email" required autocomplete="email">

                               
                            </div>
                        </div>

                        <div class="row mb-3">
                            <label for="phone" class="col-md-4 col-form-label text-md-end">Phone</label>

                            <div class="col-md-6">
                                <input id="phone" type="text" class="form-control" name="phone" v-model="user.phone"  autocomplete="phone" autofocus>
                            </div>
                        </div>

                        <div class="row mb-3">
                            <label for="image" class="col-md-4 col-form-label text-md-end">Photo</label>

                            <div class="col-md-6">
                                
                               <input ref="image" type="file" class="form-control" @change="onFileUpload">
                            </div>
                        </div>

                        <div class="row mb-3">
                            <label for="password" class="col-md-4 col-form-label text-md-end">Password</label>

                            <div class="col-md-6">
                                <input id="password" type="password" class="form-control @error('password') is-invalid @enderror" name="password"  v-model="user.password" required autocomplete="new-password">

                            </div>
                        </div>

                        <div class="row mb-3">
                            <label for="password-confirm" class="col-md-4 col-form-label text-md-end">Confirm Password</label>

                            <div class="col-md-6">
                                <input id="password-confirm" type="password" class="form-control @error('password_confirmation') is-invalid @enderror" name="password_confirmation" v-model="user.passwordconfirm" required autocomplete="new-password">
                            </div>
                        </div>

                        <div class="row mb-0">
                            <div class="col-md-6 offset-md-4">
                                <button type="submit" class="btn btn-primary">
                                    Register
                                </button>
                            </div>
                        </div>
                    </form>
                
</template>

<script>
    export default {
     data() {
            return {
                FILE: '',
            user: [],
            user: {name: '', email: '',password:'' , passwordconfirm:'', phone:'', image:''}
            }
    },
  methods:{
     onFileUpload (event) {
     this.FILE = event.target.files[0]
     },
    register() {
 
      if(this.user.name.trim() === '' || this.user.email.trim() === ''){
        alert('Debes completar todos los campos antes de guardar');
        return;
      }
console.log(this.FILE.name)
      let img = (this.FILE.name === undefined) ? null : this.FILE.name;
      console.log(img)
       const formData = new FormData()
          formData.append('image',this.FILE,img)
          formData.append('name', this.user.name)
           formData.append('email', this.user.email)
            formData.append('password', this.user.password)
             formData.append('password_confirmation', this.user.passwordconfirm)
             formData.append('phone', this.user.phone)

      axios.post('/register',formData)
        .then((res) =>{
          location.reload();
        }).catch(function(error) {
                    console.log(error)
                    
        })
    }

  }
}
</script>
