<script setup>
import { Icon } from "@iconify/vue";
import { reactive, ref } from "vue";
import { onClickOutside } from "@vueuse/core";
const ListِAppear = reactive({
  notifaction: false,
  message: false,
  userList: false,
  settings: true,
});
// Convert css variables to dark mode
const darkMode = () => {
  document.documentElement.style.setProperty("--whiteColor", "#1E293B");
  document.documentElement.style.setProperty("--Input", "#324055");
  document.documentElement.style.setProperty("--Heading", "#94A3B8");
  document.documentElement.style.setProperty("--Body-Text", "#FFFFFF");
  document.documentElement.style.setProperty("--Note", "#95989D");
  document.documentElement.style.setProperty("--Stroke", "#283548");
  document.documentElement.style.setProperty("--bg-table", "#28354852");
  document.documentElement.style.setProperty("--bg-table-1", "#28354852");
  document.documentElement.style.setProperty("--hv-item", "#ffffff24");
  document.documentElement.style.setProperty("--headerBackground", "#303b4c");
  document.documentElement.style.setProperty("--border", "#283548 ");
  document.documentElement.style.setProperty("--background", "#0F172A ");
};
// Convert css variables to light mode
const lightMode = () => {
  document.documentElement.style.setProperty("--whiteColor", "#fff");
  document.documentElement.style.setProperty("--Input", "#ecf0f4");
  document.documentElement.style.setProperty("--Heading", "#111");
  document.documentElement.style.setProperty("--Body-Text", "#575864");
  document.documentElement.style.setProperty("--Note", "#95989d");
  document.documentElement.style.setProperty("--Stroke", "#ecf0f4");
  document.documentElement.style.setProperty("--bg-table", "#f6f8fbcc");
  document.documentElement.style.setProperty("--bg-table-1", "#f7fafc");
  document.documentElement.style.setProperty("--hv-item", "#edf1f5");
  document.documentElement.style.setProperty("--headerBackground", "#eff2f6");
  document.documentElement.style.setProperty("--border", "#ecf0f4 ");
  document.documentElement.style.setProperty("--background", "#eff4f8 ");
};

// Detect Mode And Size in Local Storage
window.onload = () => {
  const checkBox = document.querySelectorAll(".form-check-input");
  const main = document.querySelector("main");
  if (localStorage.getItem("mode") == "dark") {
    darkMode();
    checkBox[0].checked = true;
  } else if (localStorage.getItem("mode") == "dark") {
    lightMode();
    checkBox[0].checked = false;
  } else {
    lightMode();
    checkBox[0].checked = false;
  }
  if (localStorage.getItem("size") == "boxed") {
    main.classList.add("container");
    checkBox[1].checked = true;
  } else if (localStorage.getItem("size") == "normal") {
    main.classList.remove("container");
    checkBox[1].checked = false;
  } else {
    main.classList.remove("container");
    checkBox[1].checked = false;
  }
};
// Toggle Listappear.notifaction on click on Notifaction Icon (Hide/Show)
const notifactionToggle = () => {
  ListِAppear.notifaction = !ListِAppear.notifaction;
};
// Toggle Listappear.message on click on Message Icon (Hide/Show)
const messageToggle = () => {
  ListِAppear.message = !ListِAppear.message;
};
// Toggle Listappear.userList on click on user Icon (Hide/Show)
const userToggle = () => {
  ListِAppear.userList = !ListِAppear.userList;
};
// value Listappear.notifacton on click outside to be false (Hide)
const hideNotifacton = () => {
  ListِAppear.notifaction = false;
};
// value Listappear.message on click outside to be false (Hide)
const hideMessage = () => {
  ListِAppear.message = false;
};
// value Listappear.userList on click outside to be false (Hide)
const hideUser = () => {
  ListِAppear.userList = false;
};
// value Listappear.settings on click outside to be false (Hide)
const closeSettings = () => {
  let settings = document.querySelector(".setting");
  settings.classList.remove("show");
};
// value Listappear.settings on click outside to be true (Show)
const openSettings = () => {
  let settings = document.querySelector(".setting");
  settings.classList.add("show");
};
// add ref for message and notifaction icon to join it with script
const notifaction = ref(null);
const message = ref(null);
const user = ref(null);

// hide message or notifactions on click outside
onClickOutside(notifaction, hideNotifacton);
onClickOutside(message, hideMessage);
onClickOutside(user, hideUser);

// Toggle website Theme (Dark / Light)
const toggleMode = () => {
  const checkBox = document.querySelectorAll(".form-check-input");
  if (checkBox[0].checked == true) {
    localStorage.setItem("mode", "dark");
    darkMode();
  } else if (checkBox[0].checked == false) {
    localStorage.setItem("mode", "light");
    lightMode();
  }
};
// Toggle website size (normal / boxed)
const toggleContainer = () => {
  const checkBox = document.querySelectorAll(".form-check-input");
  const main = document.querySelector("main");
  if (checkBox[1].checked == true) {
    localStorage.setItem("size", "boxed");
    main.classList.add("container");
  } else if (checkBox[1].checked == false) {
    localStorage.setItem("size", "normal");
    main.classList.remove("container");
  }
};

const clear = () => {
  localStorage.clear();
  location.reload();
};
</script>

<template>
  <nav class="navbar navbar-expand-lg">
    <div class="container-fluid">
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <form class="d-flex" role="search">
          <input
            class="form-control me-2 searchInput"
            type="search"
            placeholder="Search here..."
            aria-label="Search"
          /><Icon icon="mdi:magnify" height="24" />
        </form>
        <div class="right-items">
          <div class="header-item" ref="notifaction">
            <div style="cursor: pointer" class="icon-not">
              <div class="Icon-notify">1</div>
              <Icon icon="mdi:bell-outline" @click="notifactionToggle()"></Icon>
              <ul class="msg" v-if="ListِAppear.notifaction">
                <li><h6>Notifactions</h6></li>
                <li>
                  <div class="content">
                    <div class="img">
                      <Icon icon="ri:discount-percent-fill"></Icon>
                    </div>
                    <div class="info">
                      <div class="top">
                        <h3 class="msgheading">Discount available</h3>
                      </div>
                      <div class="bot">
                        <p class="msgpargraph">
                          Morbi sapien massa, ultricies at rhoncus at,
                          ullamcorper nec diam
                        </p>
                      </div>
                    </div>
                  </div>
                </li>
                <li>
                  <div class="content">
                    <div class="img">
                      <Icon icon="octicon:verified" />
                    </div>
                    <div class="info">
                      <div class="top">
                        <h3 class="msgheading">Account has been verified</h3>
                      </div>
                      <div class="bot">
                        <p class="msgpargraph">
                          Mauris libero ex, iaculis vitae rhoncus et
                        </p>
                      </div>
                    </div>
                  </div>
                </li>
                <li>
                  <div class="content">
                    <div class="img">
                      <Icon icon="material-symbols:box-rounded" />
                    </div>
                    <div class="info">
                      <div class="top">
                        <h3 class="msgheading">Order shipped successfully</h3>
                      </div>
                      <div class="bot">
                        <p class="msgpargraph">
                          Integer aliquam eros nec sollicitudin sollicitudin
                        </p>
                      </div>
                    </div>
                  </div>
                </li>
                <li>
                  <div class="content">
                    <div class="img">
                      <Icon icon="mdi:truck-delivery" />
                    </div>
                    <div class="info">
                      <div class="top">
                        <h3 class="msgheading">Order pending: ID 305830</h3>
                      </div>
                      <div class="bot">
                        <p class="msgpargraph">
                          Ultricies at rhoncus at ullamcorper
                        </p>
                      </div>
                    </div>
                  </div>
                </li>
                <li><button>View All</button></li>
              </ul>
            </div>
          </div>
          <div class="header-item" ref="message">
            <div style="cursor: pointer" class="icon-not">
              <div class="Icon-notify">1</div>
              <Icon icon="mdi:message-outline" @click="messageToggle()"></Icon>
              <ul v-if="ListِAppear.message">
                <li><h6>Messages</h6></li>
                <li>
                  <div class="content">
                    <div class="img">
                      <img src="../assets/team-01.png" alt="" srcset="" />
                    </div>
                    <div class="info">
                      <div class="top">
                        <h3>Mohamed Ahmed</h3>
                        <span class="time">10:13 PM</span>
                      </div>
                      <div class="bot">
                        <p>Hello?</p>
                      </div>
                    </div>
                  </div>
                </li>
                <li>
                  <div class="content">
                    <div class="img">
                      <img src="../assets/team-03.png" alt="" srcset="" />
                    </div>
                    <div class="info">
                      <div class="top">
                        <h3>Suhail Ahmed</h3>
                        <span class="time">10:13 PM</span>
                      </div>
                      <div class="bot">
                        <p>Are you there? interested i this...</p>
                      </div>
                    </div>
                  </div>
                </li>
                <li>
                  <div class="content">
                    <div class="img">
                      <img src="../assets/team-04.png" alt="" srcset="" />
                    </div>
                    <div class="info">
                      <div class="top">
                        <h3>Ali Ismail</h3>
                        <span class="time">10:13 PM</span>
                      </div>
                      <div class="bot">
                        <p>Interested in this loads?</p>
                      </div>
                    </div>
                  </div>
                </li>
                <li>
                  <div class="content">
                    <div class="img">
                      <img src="../assets/team-02.png" alt="" srcset="" />
                    </div>
                    <div class="info">
                      <div class="top">
                        <h3>Joe Doe</h3>
                        <span class="time">10:13 PM</span>
                      </div>
                      <div class="bot">
                        <p>Interested in this loads?</p>
                      </div>
                    </div>
                  </div>
                </li>
                <li><button>View All</button></li>
              </ul>
            </div>
          </div>
          <div class="header-item" ref="user">
            <div class="user">
              <div
                class="image"
                style="max-width: 36px; cursor: pointer"
                @click="userToggle()"
              >
                <img
                  src="../assets/team-01.png"
                  alt=""
                  srcset=""
                  style="max-width: 100%"
                />
              </div>
              <div
                class="userInfo"
                style="cursor: pointer"
                @click="userToggle()"
              >
                <span class="username">Suhail Ahmed</span>
                <span class="postion">Admin</span>
              </div>
              <ul
                class="dropdown-menu d-block mx-0 border-0 w-220px"
                data-bs-theme="white"
                v-if="ListِAppear.userList"
              >
                <li>
                  <a
                    class="dropdown-item d-flex gap-2 align-items-center"
                    href="#"
                  >
                    <Icon icon="material-symbols:person-rounded" />
                    <span class="text"> Account</span>
                  </a>
                </li>
                <li>
                  <a
                    class="dropdown-item d-flex gap-2 align-items-center"
                    href="#"
                  >
                    <Icon icon="material-symbols:mail-rounded" />

                    <span class="text"> Inbox</span>
                  </a>
                </li>
                <li>
                  <a
                    class="dropdown-item d-flex gap-2 align-items-center"
                    href="#"
                  >
                    <Icon icon="lucide:file-spreadsheet" />

                    <span class="text"> Taskboard</span>
                  </a>
                </li>
                <li>
                  <a
                    class="dropdown-item d-flex gap-2 align-items-center"
                    href="#"
                  >
                    <Icon icon="material-symbols:settings" />

                    <span class="text"> Settings</span>
                  </a>
                </li>
                <li>
                  <a
                    class="dropdown-item d-flex gap-2 align-items-center"
                    href="#"
                  >
                    <Icon icon="material-symbols:headphones-rounded" />

                    <span class="text"> Support</span>
                  </a>
                </li>
                <li>
                  <a
                    class="dropdown-item d-flex gap-2 align-items-center"
                    href="#"
                  >
                    <Icon icon="material-symbols:exit-to-app" />

                    <span class="text"> Log out</span>
                  </a>
                </li>
              </ul>
            </div>
          </div>
          <div class="header-item">
            <div class="icon">
              <Icon icon="material-symbols:settings" @click="openSettings()" />
            </div>
            <div class="setting">
              <div class="header">
                <h3>Settings</h3>
                <Icon
                  icon="material-symbols:close-rounded"
                  @click="closeSettings()"
                />
              </div>
              <div class="content">
                <div class="element">
                  <h3>Dark Mode:</h3>
                  <div class="form-check form-switch">
                    <input
                      class="form-check-input"
                      type="checkbox"
                      role="switch"
                      id="flexSwitchCheckChecked"
                      @click="toggleMode()"
                    />
                    <label
                      class="form-check-label"
                      for="flexSwitchCheckChecked"
                    ></label>
                  </div>
                </div>
                <div class="element">
                  <h3>Boxed Page:</h3>
                  <div class="form-check form-switch">
                    <input
                      class="form-check-input"
                      type="checkbox"
                      role="switch"
                      id="flexSwitchCheckChecked"
                      @click="toggleContainer"
                    />
                    <label
                      class="form-check-label"
                      for="flexSwitchCheckChecked"
                    ></label>
                  </div>
                </div>
                <div class="element">
                  <button @click="clear()">Reset</button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<style lang="css">
body {
  overflow-x: hidden;
  background-color: var(--background) !important;
}
:root {
  --mainColor: #2275fc;
  --whiteColor: #fff;
  --Input: #ecf0f4;
  --Black: #111;
  --Heading: #111;
  --Body-Text: #575864;
  --22-c-55-e: #22c55e;
  --Style: #ff5200;
  --Palette-Green-500: #22c55e;
  --Palette-Blue-Gray-300: #cbd5e1;
  --Palette-Blue-Gray-200: #e2e8f0;
  --Palette-Blue-300: #93c5fd;
  --Palette-Blue-200: #bfdbfe;
  --Palette-Orange-400: #fb923c;
  --Palette-Red-400: #f87171;
  --Palette-Red-500: #ef4444;
  --Icon: #cbd5e1;
  --Note: #95989d;
  --Text-Holder: #858b93;
  --08091-b: #08091b;
  --Stroke: #ecf0f4;
  --bg-table: #f6f8fbcc;
  --bg-table-1: #f7fafc;
  --backdrop: #f2f7fb;
  --hv-item: #edf1f5;
  --headerBackground: #eff2f6;
  --border: #ecf0f4;
}
.navbar {
  width: 100%;
  height: fit-content;
  background-color: var(--whiteColor) !important;
  padding: 15px 0 !important;
}
form {
  position: relative;
  width: 500px;
}
form > input.searchInput {
  width: 550px;
  font-size: 14px;
  padding: 7px 10px;
  background-color: transparent;
  border: 1px solid var(--Input);
  color: var(--Heading);
  &::placeholder {
    color: #818790;
  }
}
form > input.searchInput:focus {
  outline: none;
  border: none;
  box-shadow: none;
  background-color: transparent;
  border: 1px solid var(--Input) !important;
  color: var(--Heading);
}
form > svg {
  position: absolute;
  right: 5px;
  top: 6px;
  margin: 0 11px;
  color: var(--Heading);
}
.navbar-expand-lg .navbar-collapse {
  justify-content: space-between;
}
.right-items {
  display: flex;
}
.header-item:nth-child(3) {
  display: flex;
}
.header-item .userInfo {
  display: flex;
  padding-right: 30px;
  border-right: 1px solid var(--border);
  flex-direction: column;
  .username {
    font-weight: bold;
    margin-top: 4px;
    color: var(--Heading);
  }
  .postion {
    color: var(--Note);
    margin-top: -4px;
  }
}
.header-item .image {
  max-width: 36px;
  display: flex;
  align-items: center;
  height: 45px;
  margin: 0 10px;
  img {
    max-width: 36px;
    border-radius: 50%;
  }
}
.header-item .icon-not {
  display: flex;
  background-color: var(--headerBackground);
  height: 36px;
  width: 36px;
  padding: 7px;
  margin: 5px 10px;
  border-radius: 50%;
  position: relative;
  justify-content: center;
  align-items: center;
  svg {
    color: var(--Heading);
  }
  ul {
    transition: 0.3s;
    width: 300px;
    position: absolute;
    margin: 20px 0;
    padding: 16px;
    top: 22px;
    right: 12px;
    background-color: var(--whiteColor);
    box-shadow: 0px 4px 24px 2px rgba(20, 25, 38, 0.1);
    border-radius: 9px;
    &.msg .info {
      width: 100%;
    }

    li {
      button {
        width: 100%;
        border: none;
        margin-top: 10px;
        border-radius: 10px;
        color: #fff;
        font-size: 18px;
        font-weight: bold;
        padding: 5px;
        background-color: var(--mainColor);
        margin-bottom: -5px;
        transition: 0.3s;
        &:hover {
          background-color: var(--whiteColor);
          color: var(--mainColor);
          border: 1px solid var(--mainColor);
          margin-top: 8px;
          margin-bottom: -9px;
        }
      }
      &:not(:first-child) {
        margin: 15px 0;
      }
      .content {
        display: flex;
      }
      h6 {
        padding-bottom: 16px;
        border-bottom: 1px solid var(--Stroke);
        color: var(--Heading);
      }
      .img {
        width: 52px;
        height: 46px;
        align-items: center;
        display: flex;
        justify-content: center;
        background-color: #e9f2ff;
        border-radius: 50%;
        svg {
          background-color: #e9f2ff;
          font-size: 25px;
          color: var(--mainColor);
        }
        img {
          border-radius: 50%;
          max-width: 100%;
        }
      }
      .info {
        position: relative;
        top: 10px;
        .top {
          h3 {
            font-size: 12px;
            margin-left: 10px;
            width: 100px;
            color: var(--Heading);
            &.msgheading {
              width: 200px;
            }
          }
          span {
            font-size: 10px;
            margin-left: 60px;
            width: 45px;
            color: var(--Note);
          }
          display: flex;
        }
        .bot {
          p {
            margin-left: 10px;
            margin-top: -9px;
            font-size: 12px;
            color: var(--Note);
            &.msgpargraph {
              font-size: 10px;
            }
          }
        }
      }
      list-style: none;
    }
  }
}
.header-item .icon-not .Icon-notify {
  animation: pop-up 1s cubic-bezier(0, 0, 0.2, 1) infinite;
  transition: 0.3s;
  height: 16px;
  width: 16px;
  background: #2275fc;
  color: #fff !important;
  border-radius: 50%;
  color: var(--whiteColor);
  position: absolute;
  top: -3px;
  font-size: 12px;
  display: flex;
  align-content: center;
  justify-content: center;
  flex-wrap: wrap;
  right: -4px;
  font-weight: 600;
}
.header-item .user {
  position: relative;
  display: flex;

  ul {
    position: absolute;
    top: 52px;
    right: 25px;
    box-shadow: 0px 4px 24px 2px rgba(20, 25, 38, 0.1);
    background-color: var(--whiteColor) !important;
    span.text {
      font-weight: 600;
    }

    li {
      a {
        transition: 0.3s;
        color: var(--Heading) !important;
        &:hover {
          background-color: var(--whiteColor) !important;
          color: var(--mainColor) !important;
          svg {
            color: var(--mainColor);
          }
        }
      }
      svg {
        transition: 0.3s;
        color: #cbd5e1;
        font-size: 19px;
      }
    }
  }
}
.header-item:nth-child(4) {
  margin-left: 20px;
  align-items: center;
  display: flex;
  transition: 0.3s;
  .icon {
    svg {
      animation: rotate 2s infinite linear;
      font-size: 30px;
      color: var(--Body-Text);
    }
  }
  .setting {
    transition: 0.5s;
    background-color: #fff;
    box-shadow: 0px 30px 30px 2px rgba(20, 25, 38, 0.1);
    height: 100vh;
    position: absolute;
    transform: translateX(100%);
    visibility: hidden;
    top: 0;

    border-radius: 14px 0px 0px 14px;
    padding: 30px;
    &.show {
      transition: 0.5s;
      width: 360px;
      transform: translateX(-310px);
      visibility: visible;
    }
  }
  .header {
    justify-content: space-between;
    display: flex;
    margin-bottom: 20px;
    border-bottom: 1px solid #edf1f5;
    h3 {
      font-size: 24px;
      color: #111;
      font-family: Inter, sans-serif;
      align-items: center;
    }
    svg {
      font-size: 24px;
      color: #111;
    }
  }
  .content {
    .element {
      padding-bottom: 20px;
      border-bottom: 1px solid #edf1f5;
      &:nth-child(3) {
        border-bottom: none;
        padding: none;
      }
      h3 {
        font-size: 20px;
        margin-bottom: 10px;
        margin-top: 22px;
        font-weight: 500;
      }
      .form-check {
        input {
          width: 300px;
          height: 25px;
        }
      }
      button {
        border-bottom: 0px solid #edf1f5;
        bottom: 0;
        position: absolute;
        margin-bottom: 30px;
        width: 300px;
        border: none;
        background-color: var(--mainColor);
        border-radius: 7px;
        color: #fff;
        padding: 5px 0px;
        font-weight: bold;
        font-size: 20px;
        letter-spacing: 1px;
      }
    }
  }
}

@keyframes pop-up {
  0% {
    -webkit-transform: scale3d(1, 1, 1);
    transform: scale3d(1, 1, 1);
  }
  30% {
    -webkit-transform: scale3d(1.25, 0.75, 1);
    transform: scale3d(1.25, 0.75, 1);
  }
  40% {
    -webkit-transform: scale3d(0.75, 1.25, 1);
    transform: scale3d(0.75, 1.25, 1);
  }
  50% {
    -webkit-transform: scale3d(1.15, 0.85, 1);
    transform: scale3d(1.15, 0.85, 1);
  }
  65% {
    -webkit-transform: scale3d(0.95, 1.05, 1);
    transform: scale3d(0.95, 1.05, 1);
  }
  75% {
    -webkit-transform: scale3d(1.05, 0.95, 1);
    transform: scale3d(1.05, 0.95, 1);
  }
  100% {
    -webkit-transform: scale3d(1, 1, 1);
    transform: scale3d(1, 1, 1);
  }
}
@keyframes rotate {
  0% {
    rotate: 0deg;
  }
  100% {
    rotate: 360deg;
  }
}
@keyframes appearSettings {
  0% {
    right: -530px;
  }
  100% {
    right: 0;
  }
}
</style>
