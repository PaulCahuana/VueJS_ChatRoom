<template lang="html">
<div class="container">
    <div class="row">
        <div class="col-md-4 col-md-offset-4">
            <div class="panel panel-default">
                <div class="panel-heading">
                    <h3 class="panel-title">
                        Reset Your Password
                    </h3>
                </div>
                <div class="panel-body">
                    <form @submit.prevent="reset">
                        <fieldset>
                            <div class="form-group">
                                <input class="form-control" name="password" placeholder="Password at least 6 characters" type="password" value="" v-model=password v-validate="'required|min:6'">
                                </input>
                                 <div v-show="errors.has('password')" class="alert alert-danger">{{ errors.first('password') }}</div>
                            </div>
                            <div class="form-group">
                                <input class="form-control" name="password_confirmed" placeholder="Re-enter password" type="password" value="" v-validate="'required|confirmed:password'">
                                </input>
                                 <div v-show="errors.has('password_confirmed')" class="alert alert-danger">{{ errors.first('password_confirmed') }}</div>
                            </div>
                            <input class="btn btn-lg btn-primary btn-block" type="submit" value="Submit">
                            </input>
                        </fieldset>
                    </form>
                </div>
            </div>
        </div>
    </div>
</div>
</template>

<script>
export default {
  name: 'reset',
  data () {
    return {
      password: ''
    }
  },
  methods: {
    eset () {
      this.$validator.validateAll()
      if (!this.errors.any()) {
        this.$http.post('/reset/' + this.$route.params.token, {password: this.password}).then(response => {
          window.swal({
            title: 'Success!',
            text: 'Your password was saved',
            type: 'success',
            confirmButtonText: 'OK'
          })
          // Redirect to login view
          this.$router.push({ path: '/' })
        }).catch(function (error) {
          console.log(error)
          window.swal({
            title: 'Whoops!',
            text: 'Look like something went wrongs!! Try again',
            type: 'error',
            confirmButtonText: 'OK'
          })
        })
      }
    }
  }

}
</script>

<style scoped>
body{padding-top:20px;}
</style>