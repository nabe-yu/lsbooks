<template>
  <!-- ヘッダ -->
  <div class="container">
    <nav class="navbar">
      <div id="navMenu" class="navbar-menu">
        <div class="navbar-start">
          <a class="navbar-item">
            📚lsbooks
          </a>
          <a class="navbar-item">
            API
          </a>
        </div>
        <div class="navbar-end">
          <div class="navbar-item">
            <div class="buttons">
              <a class="button is-link">Add Book</a>
            </div>
          </div>
        </div>
      </div>
    </nav>

    <div class="columns">
      <div class="column is-6 is-offset-3">
        <!-- TODO: コンポーネントに切り出す -->
        <div class="card my-4">
          <div class="card-content">
            <div class="media">
              <div class="media-left">
                <figure class="image is-64x64">
                  <a href="https://www.amazon.co.jp/s?k=978-4478108536">
                    <img
                      src="https://cover.openbd.jp/9784873115658.jpg"
                      alt="Placeholder image"
                    />
                  </a>
                </figure>
              </div>

              <div class="media-content">
                <p class="title is-6">
                  リーダブルコード :リーダブルコード :リーダブルコード
                  :リーダブルコード :リーダブルコード :
                </p>
                <div class="subtitle is-6">------</div>
                <div class="field is-grouped is-grouped-multiline">
                  <div class="control">
                    <div class="tags has-addons">
                      <span class="tag is-dark">owner</span>
                      <span class="tag is-info">****</span>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <section>
      <div class="buttons">
        <b-button
          label="Launch prompt (default)"
          type="is-dark"
          size="is-medium"
          @click="prompt"
        />

        <b-button
          label="Launch prompt (number)"
          type="is-dark"
          size="is-medium"
          @click="promptNumber"
        />

        <b-button
          label="Launch prompt (Not closing default)"
          type="is-dark"
          size="is-medium"
          @click="promptNotClosed"
        />
      </div>
    </section>
  </div>
</template>

<script>
export default {
  methods: {
    prompt() {
      this.$buefy.dialog.prompt({
        message: `What's your name?`,
        inputAttrs: {
          placeholder: "e.g. Walter",
          maxlength: 10,
        },
        trapFocus: true,
        onConfirm: (value) => this.$buefy.toast.open(`Your name is: ${value}`),
      });
    },
    promptNumber() {
      this.$buefy.dialog.prompt({
        message: `What's your age?`,
        inputAttrs: {
          type: "number",
          placeholder: "Type your age",
          value: "18",
          maxlength: 2,
          min: 18,
        },
        trapFocus: true,
        onConfirm: (value) => this.$buefy.toast.open(`Your age is: ${value}`),
      });
    },
    promptNotClosed() {
      this.$buefy.dialog.prompt({
        message: "Send your message to moon 🚀",
        inputAttrs: {
          type: "text",
          placeholder: "My message is...",
          value: "Hello moon!",
        },
        confirmText: "Send",
        trapFocus: true,
        closeOnConfirm: false,
        onConfirm: (value, { close }) => {
          this.$buefy.toast.open(`Your message is sending...`);
          setTimeout(() => {
            this.$buefy.toast.open(`Success message send!`);
            close();
          }, 2000);
        },
      });
    },
  },
};
</script>

<style lang="scss">
@import "../node_modules/bulma/bulma.sass";
</style>
