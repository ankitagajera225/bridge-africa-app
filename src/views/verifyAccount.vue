<template>
  <b-container
    class="container p-2 p-md-5 h-100 w-100 mx-auto my-auto blec"
    fluid
  >
    <div class="w-100 h-100 my-auto mx-auto mt-10">
      <b-card tag="article" class="my-auto mx-auto text-center mw-30 h-100">
        <img src="../assets/logo.png" class="image" alt="" /> <br />
        <br />

        <span class="verif-text mb-5"> Verification </span>

        <div class="step-2">
          <b-card-text class="w-75 mx-auto mt-5 text-left">
            <div class="text-center">You will get an OTP by SMS</div>
          </b-card-text>
          <b-form class="w-75 mx-auto text-center">
            <md-field>
              <label for="otp"> OTP</label>
              <md-input
                type="text"
                name="otp"
                id="otp"
                v-model="token"
                required
              />
            </md-field>

            <br />

            <b-button
              class="buttonn"
              @click.prevent="Verify"
              variant="primary"
              type="submit"
            >
              Verify
            </b-button>
          </b-form>

          <p class="mt-5 mt-md-2">
            Didn't recieved the verification OTP?
            <b-link @click.prevent="resendOtp()"> Resend OTP </b-link>
          </p>
        </div>
      </b-card>
    </div>

    <FlashMessage />
  </b-container>
</template>

<script>
import { mapActions } from "vuex";
import axios from "axios";

export default {
  data() {
    return {
      token: ""
    };
  },
  methods: {
    resendOtp() {
      console.log(this.$store.state.auth.user.user.phone);
      axios
        .post("user/resendOtp", {
          phone: this.$store.state.auth.user.user.phone
        })
        .then(response => {
          if (response.status === 200) {
            console.log("response: ",response);
            this.flashMessage.show({
              status: "success",
              title: "Successfully Send",
              message: "SMS successfully send check your inbox"
            });
          } else {
            console.log(response.data);
          }
        })
        .catch(err => {
          console.log({ err: err });

          this.flashMessage.show({
            status: "error",
            title: "Send Failed",
            message: "Message not send"
          });
        });
    },

    Verify() {
      console.log(this.$store.state.auth.user.user.phone);
      this.$store
        .dispatch("auth/verify", {
          OTP: this.token,

          phone: this.$store.state.auth.user.user.phone
        })
        .then(response => {
          this.$router.push({ name: "welcome" });
        })
        .catch(err => {
          console.log({ err: err });

          this.flashMessage.show({
            status: "error",
            title: "Verification Failed",
            message: "Unable to verify your account"
          });
        });
    }
  }
};
</script>

<style scoped>
.verif-text {
  font-size: 30px;
  margin-top: 10px;
}
.image {
  width: 50%;
}

.buttonn {
  width: 150px !important;
}

.mw-30 {
  max-width: 30rem;
}

@media only screen and (max-width: 768px) {
  .image {
    width: 75%;
  }

  .mt-10 {
    margin-top: 10px !important;
  }

  .card-body {
    margin-top: 30px !important;
    padding-bottom: 100px !important;
  }
}
</style>
