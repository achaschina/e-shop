<template>
  <div>
    <b-navbar toggleable="md" type="dark" variant="info">
      <b-navbar-toggle target="nav_collapse"></b-navbar-toggle>

      <b-navbar-brand to="/">
        <img src="../../assets/logo.png" style="height:30px;" @click="active_el=0">
      </b-navbar-brand>

      <b-collapse is-nav id="nav_collapse">
        <div style="">
          <ul class="navbar-nav">
            <li
              class="nav-item nav-level-1"
              data-category-id="1"
              @click="route({path: '/women'}, 1)"
              @mouseover="showMenu=true"
              :class="{ active : active_el == 1}"
            >Она
            <!-- <span class="first-level"></span> -->
              <div class="nav-level2">
                <b-row>
                  <b-col cols="2" class="sidenav">
                    <div
                      class="sidenav-item"
                      @mouseover="active_nav_el=1"
                      :class="{ sidenavActive : active_nav_el == 1}"
                    >Одежда</div>
                    <div
                      class="sidenav-item"
                      @mouseover="active_nav_el=2"
                      :class="{ sidenavActive : active_nav_el == 2}"
                    >Обувь</div>
                    <div
                      class="sidenav-item"
                      @mouseover="active_nav_el=3"
                      :class="{ sidenavActive : active_nav_el == 3}"
                    >Аксесуары</div>
                    <div
                      class="sidenav-item"
                      @mouseover="active_nav_el=4"
                      :class="{ sidenavActive : active_nav_el == 4}"
                    >Sale</div>
                  </b-col>
                  <b-col cols="10" class="sidenav-content">{{msg}}</b-col>
                </b-row>
              </div>
            </li>
            <li
              class="nav-item nav-level-1"
              data-category-id="2"
              @click="route({path: '/men'}, 2)"
              :class="{ active : active_el == 2}"
            >Он
              <div class="nav-level2">
                <b-row>
                  <b-col cols="2" class="sidenav">
                    <div
                      class="sidenav-item"
                      @mouseover="active_nav_el=1"
                      :class="{ sidenavActive : active_nav_el == 1}"
                    >ОдеждаFF</div>
                    <div
                      class="sidenav-item"
                      @mouseover="active_nav_el=2"
                      :class="{ sidenavActive : active_nav_el == 2}"
                    >Обувь</div>
                    <div
                      class="sidenav-item"
                      @mouseover="active_nav_el=3"
                      :class="{ sidenavActive : active_nav_el == 3}"
                    >Аксесуары</div>
                    <div
                      class="sidenav-item"
                      @mouseover="active_nav_el=4"
                      :class="{ sidenavActive : active_nav_el == 4}"
                    >Sale</div>
                  </b-col>
                  <b-col cols="10" class="sidenav-content">{{msg}}</b-col>
                </b-row>
              </div>
            </li>
            <li
              class="nav-item"
              data-category-id="3"
              @click="route({path: '/children'}, 3)"
              :class="{ active : active_el == 3}"
            >Дети</li>
            <li
              class="nav-item"
              data-category-id="4"
              @click="route({path: '/sale'}, 4)"
              :class="{ active : active_el == 4}"
            >Sale</li>
          </ul>
        </div>

        <b-navbar-nav class="ml-auto">
          <b-nav-form>
            <b-button size="sm" class="my-2 my-sm-0" @click="showModal">{{loginBtn}}</b-button>
          </b-nav-form>
          <b-nav-item-dropdown right>
            <template slot="button-content">
              <em>{{currentUserName}}</em>
            </template>
            <b-dropdown-item href="#">Profile</b-dropdown-item>
            <b-dropdown-item @click="signout()">Вийти</b-dropdown-item>
          </b-nav-item-dropdown>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>

    <div class="breadcrumbs"></div>

    <AuthComponent
      v-model="modal"
      :modal-show="modal.show"
      @updateCurrenUserName="updateUserName"
      @updateLoginButton="updateLoginButton"
    ></AuthComponent>

    <b-alert
      :show="dismissCountDown"
      dismissible
      variant="warning"
      @dismissed="dismissCountDown=0"
      @dismiss-count-down="countDownChanged"
    >
      <p>{{messegeAlert}}</p>
    </b-alert>
  </div>
</template>

<script>
import AuthComponent from "./authentication/Authentication.vue";
import Authentication from "./index.js";
export default {
  components: {
    AuthComponent
  },
  data() {
    return {
      modal: {
        show: false
      },
      loginBtn: "Логін",
      currentUserName: "",
      snackbar: false,
      dismissSecs: 5,
      dismissCountDown: 0,
      messegeAlert: "",
      show: true,
      showMenu: false,
      active_el: 0,
      active_nav_el: 0,
      msg: ""
    };
  },
  methods: {
    route(path, el) {
      this.$router.push(path);
      this.active_el = el;
    },
    activeCategory(e) {
      for (
        var i = 0, atts = e.target.attributes, n = atts.length, arr = [];
        i < n;
        i++
      ) {
        if (atts[i].nodeName == "data-category-id") {
          this.msg = atts[i].nodeValue;
        }
      }
    },
    updateUserName(v) {
      this.currentUserName = v;
    },
    updateLoginButton(v) {
      this.loginBtn = v;
    },
    showModal() {
      this.modal.show = true;
    },

    countDownChanged(dismissCountDown) {
      this.dismissCountDown = dismissCountDown;
    },

    signout() {
      Authentication.signout(this, "/");
    }
  },
  mounted() {
    $(".nav-item.nav-level-1").hover(
      function() {
        $($(this).children()[0])
          .addClass("hover")
          .hover(function() {
            $($(this).children()[0]).addClass("hover");
          }),
          function() {
            $($(this).children()[0]).removeClass("hover");
          };
      },
      function() {
        $($(this).children()[0]).removeClass("hover");
      }
    );
  }
};
</script>

<style scoped lang="css" >
.navbar {
  background: #ffffff !important;
  border-bottom: 1px solid #e5e5e5;
}
.navbar-nav > .nav-item {
  /* position: relative; */
  color: black !important;
  font-size: 21px;
  font-family: "Oswald", sans-serif;
  padding: 0 10px 0;
}
.navbar-nav > .nav-item.active {
  color: #be9e56 !important;
}
.nav-level2 {
  display: none;
  position: absolute;
  min-height: 150px;
  /* top: 100%; */
  left: 0;
  width: 100vw;
  padding: 0 15px 0 0;
  background: #fff;
  border-top: 1px #e5e5e5 solid;
  z-index: 10000000;
  -webkit-box-shadow: 0 5px 7px rgba(0, 0, 0, 0.1);
  -moz-box-shadow: 0 5px 7px rgba(0, 0, 0, 0.1);
  box-shadow: 0 5px 7px rgba(0, 0, 0, 0.1);
}
.hover {
  display: block;
  z-index: 10000000;
}
.row.hover {
  display: flex !important;
}
.sidenav-item {
  padding: 15px;
  border-bottom: 1px #e5e5e5 solid;
  border-top: none;
  text-align: center;
  font-family: "Oswald", sans-serif;
  font-size: 21px;
  color: black !important;
}

.sidenav {
  padding-bottom: 5rem;
}
.sidenav-content,
.sidenavActive {
  background: #e5e5e5;
  font-size: 20px;
  color: #424242;
}
.col-2,
.col-10 {
  padding-left: 0;
  padding-right: 0;
}
.nav-level-1 {
    padding: 35px 10px 0;
    height: inherit;
    color: #000;
    text-decoration: none;
    font-size: 16px;
    background: transparent url('../../assets/mainNavArrow.png') 50% 1200% no-repeat;
    -webkit-transition: all .3s ease;
    -moz-transition: all .3s ease;
    -o-transition: all .3s ease;
    -ms-transition: all .3s ease;
    transition: all .3s ease;
    -o-transform: translate(0);
}
.nav-level-1:hover {
  background-position: 50% 100%;
    color: #000;
    /* opacity: .7; */
}
</style>


