<template>
  <div :style="displayed()">
    <div class="mfp-bg my-mfp-zoom-in mfp-ready"></div>
    <div
      class="mfp-wrap mfp-close-btn-in mfp-auto-cursor my-mfp-zoom-in mfp-ready"
      tabindex="-1"
    >
      <div class="mfp-container mfp-inline-holder">
        <div class="mfp-content">
          <div id="login-register-popup" class="small-dialog zoom-anim-dialog">
            <!-- ===== Start of Signin wrapper ===== -->
            <div class="signin-wrapper">
              <div class="small-dialog-headline">
                <h4 class="text-center">Sign in</h4>
              </div>

              <div class="small-dialog-content">
                <!-- Start of Login form -->
                <form id="cariera_login" method="post">
                  <p class="status"></p>

                  <div class="form-group">
                    <label for="username">Username or Email *</label>
                    <input
                      type="text"
                      class="form-control"
                      id="username"
                      name="username"
                      placeholder="Your Username or Email *"
                    />
                  </div>

                  <div class="form-group">
                    <label for="password">Password *</label>
                    <input
                      type="password"
                      class="form-control"
                      id="password"
                      name="password"
                      placeholder="Your Password *"
                    />
                  </div>

                  <div class="form-group">
                    <div class="checkbox pad-bottom-10">
                      <input
                        id="check1"
                        type="checkbox"
                        name="remember"
                        value="yes"
                      />
                      <label for="check1">Keep me signed in</label>
                    </div>
                  </div>

                  <div class="form-group">
                    <input
                      type="submit"
                      value="Sign in"
                      class="btn btn-main btn-effect nomargin"
                    />
                  </div>
                </form>
                <!-- End of Login form -->

                <div class="bottom-links">
                  <span>
                    Not a member?
                    <a class="signUpClick">Sign up</a>
                  </span>
                  <a class="forgetPasswordClick pull-right">Forgot Password</a>
                </div>
              </div>
            </div>
            <!-- ===== End of Signin wrapper ===== -->

            <!-- ===== Start of Signup wrapper ===== -->
            <div class="signup-wrapper">
              <div class="small-dialog-headline">
                <h4 class="text-center">Sign Up</h4>
              </div>

              <div class="small-dialog-content">
                <!-- Start of Registration form -->
                <form id="cariera_registration" action="#" method="POST">
                  <p class="status"></p>

                  <div class="form-group">
                    <label for="movify_user_login">Username</label>
                    <input
                      name="movify_user_login"
                      id="movify_user_login"
                      class="form-control"
                      type="text"
                    />
                  </div>

                  <div class="form-group">
                    <label for="movify_user_email">Email</label>
                    <input
                      name="movify_user_email"
                      id="movify_user_email"
                      class="form-control"
                      type="email"
                    />
                  </div>

                  <div class="form-group">
                    <label for="password">Password</label>
                    <input
                      name="movify_user_pass"
                      id="movify_password"
                      class="form-control"
                      type="password"
                    />
                  </div>

                  <div class="form-group">
                    <input
                      type="submit"
                      class="btn btn-main btn-effect nomargin"
                      value="Register"
                    />
                  </div>
                </form>
                <!-- End of Registration form -->

                <div class="bottom-links">
                  <span>
                    Already have an account?
                    <a class="signInClick">Sign in</a>
                  </span>

                  <a class="forgetPasswordClick pull-right">Forgot Password</a>
                </div>
              </div>
              <!-- .small-dialog-content -->
            </div>
            <!-- ===== End of Signup wrapper ===== -->

            <!-- ===== Start of Forget Password wrapper ===== -->
            <div class="forgetpassword-wrapper">
              <div class="small-dialog-headline">
                <h4 class="text-center">Forgotten Password</h4>
              </div>

              <div class="small-dialog-content">
                <!-- Start of Forger Password form -->
                <form id="forget_pass_form" action="#" method="post">
                  <p class="status"></p>

                  <div class="form-group">
                    <label for="password">Email Address *</label>
                    <input
                      type="email"
                      name="user_login"
                      class="form-control"
                      id="email3"
                      placeholder="Email Address *"
                    />
                  </div>

                  <div class="form-group">
                    <input
                      type="submit"
                      name="submit"
                      value="Get New Password"
                      class="btn btn-main btn-effect nomargin"
                    />
                  </div>
                </form>
                <!-- End of Forger Password form -->

                <div class="bottom-links">
                  <a class="cancelClick">Cancel</a>
                </div>
              </div>
              <!-- .small-dialog-content -->
            </div>
            <!-- ===== End of Forget Password wrapper ===== -->

            <button
              title="Close (Esc)"
              type="button"
              class="mfp-close"
              @click="close"
            ></button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    display: {
      type: Boolean,
      default() {
        return false;
      },
    },
  },
  methods: {
    displayed() {
      if (this.display === true) {
        return "display: block";
      } else {
        return "display: none";
      }
    },
    close(e) {
      e.preventDefault();
      this.$emit("close");
    },
  },
};
</script>

<style lang="scss" scoped></style>
