<template>
  <div class="container user-page">
    <b-form @submit="onSubmit" @reset="onReset" v-if="show">
      <b-form-group
        class="user-page__email"
        id="input-group-1"
        label="Email address:"
        label-for="input-1"
        description="We'll never share your email with anyone else."
      >
        <b-form-input
          
          id="input-1"
          v-model="form.email"
          type="email"
          placeholder="Enter email"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group 
        class="user-page__name"
        id="input-group-2" 
        label="Your Name:" 
        label-for="input-2"
      >
        <b-form-input
        
          id="input-2"
          v-model="form.name"
          placeholder="Enter name"
          required
        >
        </b-form-input>
      </b-form-group>

      <b-button class="user-page__btn" type="submit" variant="primary">Submit</b-button>
      <b-button class="user-page__btn" type="reset" variant="danger">Reset</b-button>
    </b-form>
  </div>
</template>

<script>
  export default {
    name: 'UserPage',
    data() {
      return {
        form: {
          email: '',
          name: '',
        },
        show: true
      }
    },
    methods: {
      onSubmit(event) {
        event.preventDefault()
        alert(JSON.stringify(this.form))
      },
      onReset(event) {
        event.preventDefault()
        // Reset our form values
        this.form.email = ''
        this.form.name = ''
                // Trick to reset/clear native browser form validation state
        this.show = false
        this.$nextTick(() => {
          this.show = true
        })
      }
    }
  }
</script>

<style lang="scss" scoped>
  .user-page {
    max-width: 700px;
    padding-top: 20px;

    &__name {
      padding-top: 20px;
    }

    &__btn {
      margin: 10px 5px;
    }
  }
</style>