<template>
  <div class="content">
    <div class="content-main content-left">
      <div class="error-message">
        <h2 v-show="!email.valid">Oh, please enter a valid email address.</h2>
      </div>
      <p class="title">Vue Contact Form</p>
      <div>
        <h3>Name</h3>
        <input type="text" v-model="name" />
      </div>
      <div>
        <h3>Email</h3>
        <input
          type="email"
          v-model="email.value"
          :class="{ email, error: !email.valid }"
        />
      </div>
      <div class="select-member">
        <h3>Team Member</h3>
        <select class="team-member" v-model="selection.member">
          <option value="0">Lion</option>
          <option value="1">Lewis</option>
          <option value="2">Brian</option>
        </select>
      </div>
      <div>
        <h3>Framework</h3>
        <ul class="form-list">
          <li>
            <input
              type="radio"
              id="radio-1"
              value="angular"
              v-model="selection.framework"
            />
            <label for="radio-1">Angular</label>
          </li>
          <li>
            <input
              type="radio"
              id="radio-2"
              value="react"
              v-model="selection.framework"
            />
            <label for="radio-2">ReactJS</label>
          </li>
          <li>
            <input
              type="radio"
              id="radio-3"
              value="vue"
              v-model="selection.framework"
            />
            <label for="radio-3">VueJS</label>
          </li>
        </ul>
      </div>
      <div>
        <h3>Features</h3>
        <ul class="form-list">
          <li v-for="(item, index) in features" :key="item">
            <input
              type="checkbox"
              :id="'feature-' + index"
              :value="item"
              v-model="selection.features"
            />
            <label :for="'feature-' + index">{{ item }}</label>
          </li>
          <li>
            <input type="checkbox" id="check-all" @change="checkAll($event)" />
            <label for="check-all">Check All</label>
          </li>
        </ul>
      </div>
      <div>
        <h3>Message with Counter</h3>
        <textarea
          required="required"
          maxlength="255"
          class="message"
          v-model="message.text"
        ></textarea>
        <span class="counter">{{ message.text.length }} / 255</span>
      </div>
      <div>
        <input
          type="submit"
          class="btn-submit"
          :v-model="submitted"
          @click="submitted = true"
          value="Send Form"
        />
      </div>
    </div>
    <div class="content-main content-right">
      <pre><code>{{ $data }}</code></pre>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      name: "Lion",
      email: {
        value: "lionit@gmail.com",
        valid: true,
      },
      features: ["Reactivity", "Encapsulation", "Data Binding"],
      selection: {
        member: "0",
        framework: "vue",
        features: [],
      },
      message: {
        text: `Dear Mr. President,\n...`,
        maxlength: 255,
      },
      submitted: false,
    };
  },
  methods: {
    checkAll($event) {
      if ($event.target.checked) {
        this.selection.features = this.features;
      } else {
        this.selection.features = [];
      }
    },
    validate(type, value) {
      if (type === "email") {
        this.email.valid = this.isEmail(value) ? true : false;
      }
      if (type === "type muon check") {
        //do something here
      }
    },
    isEmail: function (value) {
      var emailRegExp =
        /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      return emailRegExp.test(value);
    },
  },
  watch: {
    "email.value": function (value) {
      this.validate("email", value);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
.content {
  display: flex;
  justify-content: space-around;
  padding: 50px 0;
  color: rgb(99, 97, 97);
  .content-main {
    display: flex;
    flex-direction: column;
    flex-wrap: nowrap;
    border-radius: 5px;
    width: 500px;
    overflow: hidden;
    div {
      margin-bottom: 15px;
      textarea {
        width: 100%;
        min-height: 120px;
        border: 1px solid #cfd9db;
        border-radius: 0.25em;
        &:focus {
          outline: 1px solid #636464;
          border: none;
        }
      }
      .form-list {
        input {
          zoom: 1, 5;
        }
      }
    }
    .title {
      margin-bottom: 25px;
    }
    input[type="radio"],
    input[type="checkbox"] {
      opacity: 0;
      z-index: 2;
    }
    input[type="radio"] + label {
      transition: all 3s linear;
      position: relative;
      padding-left: 15px;
      &::before {
        content: "";
        position: absolute;
        background-color: #fff;
        border: 1px solid #ccc;
        width: 16px;
        height: 16px;
        border-radius: 50%;
        top: 2px;
        left: -15px;
      }
    }
    input[type="radio"]:checked + label {
      &::before {
        position: absolute;
        background-color: rgb(32, 45, 53);
        box-shadow: 0 0 5px rgba(44, 151, 222, 0.7);
        animation: cd-bounce 0.3s;
        width: 16px;
        height: 16px;
        border: none;
        background-image: url(data:image/svg+xml;charset=utf-8,%3C%3Fxml%20version%3D%221.0%22%20encoding%3D%22utf-8%22%3F%3E%0D%0A%3C%21DOCTYPE%20svg%20PUBLIC%20%22-%2F%2FW3C%2F%2FDTD%20SVG%201.1%2F%2FEN%22%20%22http%3A%2F%2Fwww.w3.org%2FGraphics%2FSVG%2F1.1%2FDTD%2Fsvg11.dtd%22%3E%0D%0A%3Csvg%20version%3D%221.1%22%20id%3D%22Layer_1%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20xmlns%3Axlink%3D%22http%3A%2F%2Fwww.w3.org%2F1999%2Fxlink%22%20x%3D%220px%22%20y%3D%220px%22%0D%0A%09%20width%3D%2216px%22%20height%3D%2216px%22%20viewBox%3D%220%200%2016%2016%22%20enable-background%3D%22new%200%200%2016%2016%22%20xml%3Aspace%3D%22preserve%22%3E%0D%0A%3Ccircle%20fill%3D%22%23FFFFFF%22%20cx%3D%228%22%20cy%3D%228%22%20r%3D%223%22%2F%3E%0D%0A%3C%2Fsvg%3E);
        border-radius: 50%;
        top: 2px;
        left: -15px;
      }
    }
    input[type="checkbox"] + label {
      transition: all 3s linear;
      position: relative;
      padding-left: 15px;
      &::before {
        content: "";
        position: absolute;
        background-color: #fff;
        border: 1px solid #ccc;
        width: 16px;
        height: 16px;
        border-radius: 5px;
        top: 2px;
        left: -15px;
      }
    }
    input[type="checkbox"]:checked + label {
      &::before {
        position: absolute;
        background-color: rgb(32, 45, 53);
        box-shadow: 0 0 5px rgba(44, 151, 222, 0.7);
        animation: cd-bounce 0.3s;
        width: 16px;
        height: 16px;
        border: none;
        background-image: url(data:image/svg+xml;charset=utf-8,%3C%3Fxml%20version%3D%221.0%22%20encoding%3D%22utf-8%22%3F%3E%0D%0A%3C%21--%20Generator%3A%20Adobe%20Illustrator%2018.1.1%2C%20SVG%20Export%20Plug-In%20.%20SVG%20Version%3A%206.00%20Build%200%29%20%20--%3E%0D%0A%3C%21DOCTYPE%20svg%20PUBLIC%20%22-%2F%2FW3C%2F%2FDTD%20SVG%201.1%2F%2FEN%22%20%22http%3A%2F%2Fwww.w3.org%2FGraphics%2FSVG%2F1.1%2FDTD%2Fsvg11.dtd%22%3E%0D%0A%3Csvg%20version%3D%221.1%22%20id%3D%22Layer_1%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20xmlns%3Axlink%3D%22http%3A%2F%2Fwww.w3.org%2F1999%2Fxlink%22%20x%3D%220px%22%20y%3D%220px%22%0D%0A%09%20width%3D%2216px%22%20height%3D%2216px%22%20viewBox%3D%220%200%2016%2016%22%20enable-background%3D%22new%200%200%2016%2016%22%20xml%3Aspace%3D%22preserve%22%3E%0D%0A%3Cpolyline%20fill%3D%22none%22%20stroke%3D%22%23FFFFFF%22%20stroke-width%3D%222%22%20stroke-linecap%3D%22square%22%20stroke-miterlimit%3D%2210%22%20points%3D%225%2C8%207%2C10%2011%2C6%20%22%2F%3E%0D%0A%3C%2Fsvg%3E);
        border-radius: 5px;
        top: 2px;
        left: -15px;
      }
    }
  }
  h3 {
    font-size: 16px;
    color: rgb(176, 178, 180);
    font-weight: 400;
    margin-bottom: 10px;
  }
  input[type="text"],
  input[type="email"] {
    height: 40px;
    width: 100%;
    padding: 0px 10px;
    color: rgb(54, 53, 53);
    border-radius: 5px;
    border: 1px solid #ececec;
    &:focus {
      outline: none;
      border: 1px rgb(92, 89, 89) solid;
    }
  }
  .team-member {
    height: 40px;
    width: 100%;
    padding: 0px 10px;
    border-radius: 5px;
    border: 1px solid #ececec;
    appearance: none;
    &:focus {
      outline: none;
      border: 1px rgb(92, 89, 89) solid;
    }
  }
  .select-member {
    position: relative;
    &::after {
      content: "";
      position: absolute;
      z-index: 1;
      right: 10px;
      top: 50%;
      margin-top: 8px;
      display: block;
      width: 16px;
      height: 16px;
      background: url(data:image/svg+xml;charset=utf-8,%3C%3Fxml%20version%3D%221.0%22%20encoding%3D%22utf-8%22%3F%3E%0D%0A%3C%21DOCTYPE%20svg%20PUBLIC%20%22-%2F%2FW3C%2F%2FDTD%20SVG%201.1%2F%2FEN%22%20%22http%3A%2F%2Fwww.w3.org%2FGraphics%2FSVG%2F1.1%2FDTD%2Fsvg11.dtd%22%3E%0D%0A%3Csvg%20version%3D%221.1%22%20id%3D%22Layer_1%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20xmlns%3Axlink%3D%22http%3A%2F%2Fwww.w3.org%2F1999%2Fxlink%22%20x%3D%220px%22%20y%3D%220px%22%0D%0A%09%20width%3D%2216px%22%20height%3D%2216px%22%20viewBox%3D%220%200%2016%2016%22%20enable-background%3D%22new%200%200%2016%2016%22%20xml%3Aspace%3D%22preserve%22%3E%0D%0A%3Cg%3E%0D%0A%09%3Cpolygon%20fill%3D%22%232c3e50%22%20points%3D%220.9%2C5.5%203.1%2C3.4%208%2C8.3%2012.9%2C3.4%2015.1%2C5.5%208%2C12.6%20%09%22%2F%3E%0D%0A%3C%2Fg%3E%0D%0A%3C%2Fsvg%3E)
        no-repeat center center;
      pointer-events: none;
    }
  }
  .content-left {
    padding: 25px 30px;
    background-color: #fff;
    p {
      border-bottom: 1px rgb(226, 222, 222) solid;
      color: rgb(19, 18, 18);
      padding-bottom: 10px;
    }
    ul {
      list-style: none;
      li {
        display: inline-block;
        margin-right: 20px;
      }
    }
  }
  .content-right {
    padding: 25px 30px;
    background: #19142c;
  }
  .btn-submit {
    padding: 12px 20px;
    background: #2c3e50;
    border-radius: 0.25em;
    color: #ffffff;
    font-weight: bold;
    float: right;
    cursor: pointer;
    border: none;
    position: relative;
  }
  .error {
    border-color: #e94b35 !important;
  }
  .error-message {
    height: 35px;
    margin: 0px;
    margin-bottom: 30px !important;
    h2 {
      padding: 10px 30px;
      background-color: #e94b35;
      border-radius: 8px;
      font-size: 20px;
      color: white;
    }
  }
  pre {
    color: #ffffff;
    font-size: 18px;
    line-height: 30px;
    font-family: "Source Code Pro", monospace;
    font-weight: 300;
    white-space: pre-wrap;
    opacity: 0.7;
  }
  input[type="submit"] {
    transition: all 0.1s linear;
  }
  input[type="submit"]:active {
    transform: scale(0.9);
  }
  @keyframes cd-bounce {
    0%,
    100% {
      -webkit-transform: scale(1);
    }
    50% {
      -webkit-transform: scale(0.8);
    }
  }
}
</style>
