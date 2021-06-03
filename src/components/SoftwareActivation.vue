<template>
  <!-- <h1>{{ msg }}</h1> -->
  <div id="block">
    <div class="instructions">
      <p>
        To complete the activation using the request file method, follow these
        steps:
      </p>
      <ol>
        <li>
          Click below and browse to and select the request file you saved from
          the activation wizard.
        </li>
        <li>Click Submit. A response file is generated.</li>
        <li>Save the response file to a location on your computer.</li>
        <li>Return to the activation wizard and click Import Response File.</li>
        <li>Follow the on-screen instructions to complete the activation.</li>
      </ol>
    </div>
    <div id="buttons">
      <b-form-file
        placeholder="Click browse or drop a file"
        v-on:input="inputTest"
        accept=".jpg, .png, .gif"
        v-on:change="uploaded"
        v-model="input"
        ref="file"
      ></b-form-file>

      <b-button
        id="submitBtn"
        class="btn-sft"
        v-on:click="handleSubmit"
        variant="success"
        :disabled="inputUploaded == false"
        >Submit <span id="tooltip"> Upload a file to submit</span></b-button
      >
    </div>
  </div>
</template>

<script>
const axios = require("axios");
export default {
  props: ["file"],
  data() {
    return { input: null, inputUploaded: false, fileKey: "" };
  },
  methods: {
    inputTest: function () {
      if (this.$refs.file.files[0].name.slice(-4) === this.$props.file) {
        this.inputUploaded = true;
      }
      console.log(this.$refs.file.files[0].name);
    },
    uploaded: function (e) {
      if (e.target.nodeName === "INPUT") {
        if (e.target.value.slice(-4) !== this.$props.file) {
          e.target.value = null;
          alert("Please, choose the correct file extension");
          this.inputUploaded = false;
        } else {
          console.log("line 58");
          this.inputUploaded = true;
        }
      }
      // if (e.target.nodeName === "LABEL") {
      //   console.log(
      //     document.getElementsByClassName("form-file-text")[0].innerText
      //   );
      // }
    },
    handleSubmit: function () {
      this.fileKey = this.$refs.file.files[0];
      console.log("Submit");
      console.log(this.fileKey);

      let formData = new FormData();
      formData.append("file", this.fileKey);

      axios
        .post("/_api/ManualActivationFile/Submit", formData, {
          headers: {
            "Content-type": "multipart/form/data",
          },
        })
        .then(() => console.log("success*"))
        .catch((err) => console.log(err));
    },
  },
};
</script>

<style>
#block {
  display: flex;
  flex-direction: column;
  align-items: center;
}
#tooltip {
  visibility: hidden;
  background-color: black;
  color: #fff;
  text-align: center;
  padding: 1em;
  border-radius: 6px;
  position: absolute;
  z-index: 1;
}
#submitBtn:hover:disabled #tooltip {
  visibility: visible;
}
#submitBtn:disabled {
  background-color: grey;
  color: black;
  border: hidden;
}

.btn-sft {
  width: 10em;
  margin-left: 1em;
}
#buttons {
  display: flex;
}
.instructions {
  padding: 3em 1em 1em 1em;
  text-align: left;
  font-size: 1.5em;
}
</style>
