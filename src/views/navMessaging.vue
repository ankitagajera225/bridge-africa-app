<template>
  <div>
    <Navbar />
    <b-container>
      <div class="chat-box">
        <b-row>
          <b-col class="pr-0" cols="12" xl="4" v-if="show">
            <div class="right-mobile">
              <b-row>
                <b-col>
                  <b-avatar
                    class="d-inline-block profile-pic"
                    variant="primary"
                    src="https://i.pinimg.com/originals/ee/bb/d0/eebbd0baab26157ff9389d75ae1fabb5.jpg"
                  ></b-avatar>
                </b-col>
                <b-col>
                  <h4 class="title m-10">Messages</h4>
                </b-col>
                <b-col>
                  <b-icon
                    @click="newMessage(true)"
                    class="new-message primary icon-size m-10 float-right"
                    icon="pencil-square"
                  ></b-icon>
                </b-col>
              </b-row>
              <b-container>
                <input
                  type="text"
                  class="form-control input-background"
                  placeholder="Search inbox"
                />
              </b-container>
            </div>
            <div>
              <div class="messages-mobile">
                <b-row
                  v-for="message in messages"
                  :key="message.id"
                  class="p-2 message"
                  @click="showMessages(false)"
                >
                  <b-col class="col-10">
                    <span style="display:inline-flex mb-2">
                      <b-avatar
                        class="d-inline-block profile-pic"
                        variant="primary"
                        src="https://i.pinimg.com/originals/ee/bb/d0/eebbd0baab26157ff9389d75ae1fabb5.jpg"
                      ></b-avatar>

                      <h6 class="d-inline-block ml-2  ">
                        <b class="bold"> {{ message.name }}</b>
                        <p class="duration">{{ message.startMessage }}</p>
                      </h6>
                    </span>
                  </b-col>

                  <b-col class="col-2 text-center">
                    <small> {{ message.timeStamp }} </small>
                    <p class="">
                      <b-badge variant="info">
                        {{ message.messageCount }}
                      </b-badge>
                    </p>
                  </b-col>
                </b-row>
              </div>
            </div>
          </b-col>

          <b-col class="pr-0">
            <div class="right ">
              <b-row>
                <b-col class="p-2">
                  <b-avatar
                    class="d-inline-block profile-pic"
                    variant="primary"
                    src="https://i.pinimg.com/originals/ee/bb/d0/eebbd0baab26157ff9389d75ae1fabb5.jpg"
                  ></b-avatar>
                </b-col>
                <b-col>
                  <h3 class="mt-4 title">Messages</h3>
                </b-col>
                <b-col>
                  <b-icon
                    @click="newMessage(true)"
                    class="new-message primary icon-size float-right"
                    icon="pencil-square"
                  ></b-icon>
                </b-col>
              </b-row>
              <input
                type="text"
                class="form-control input-background"
                placeholder="Search inbox"
              />
            </div>
            <div>
              <div class="messages">
                <b-row
                  v-for="message in messages"
                  :key="message.id"
                  class="p-2 message"
                  @click="showInfo(false)"
                >
                  <b-col class="col-9">
                    <span style="display:inline-flex">
                      <b-avatar
                        class="d-inline-block profile-pic"
                        variant="primary"
                        src="https://i.pinimg.com/originals/ee/bb/d0/eebbd0baab26157ff9389d75ae1fabb5.jpg"
                      ></b-avatar>

                      <h6 class="mt-2  d-inline-block ml-2  ">
                        <b class="bold"> {{ message.name }}</b>
                        <p class="duration">{{ message.startMessage }}</p>
                      </h6>
                    </span>
                  </b-col>

                  <b-col class="col-3 text-center">
                    <small class="text-center"> {{ message.timeStamp }} </small>
                    <p class="text-center">
                      <b-badge variant="info">
                        {{ message.messageCount }}
                      </b-badge>
                    </p>
                  </b-col>
                </b-row>
              </div>
            </div>
          </b-col>
          <b-col
            v-if="show == false && info == false && newMsg == false"
            class="p-0 back-image "
            cols="12"
            xl="8"
            style="margin-right: 14px;"
          >
            <div class="">
              <div class="chat-nav shadow ">
                <b-row class="mobile">
                  <b-col class="col-1">
                    <b-icon
                      @click="showMessages(true)"
                      icon="arrow-left"
                      aria-hidden="true"
                      class="primary "
                    ></b-icon>
                  </b-col>
                  <b-col class="col-3">
                    <b-avatar
                      variant="primary"
                      src="https://i.pinimg.com/originals/ee/bb/d0/eebbd0baab26157ff9389d75ae1fabb5.jpg"
                      size="40"
                    ></b-avatar>
                  </b-col>

                  <b-col class="detale">
                    <h6>Louis Litt</h6>
                    <small>Online</small>
                  </b-col>
                  <b-col cols="3">
                    <b-row class="mt-3">
                      <b-col class="col-3">
                        <b-icon icon="search" class="primary"></b-icon>
                      </b-col>
                      <b-col class="col-3">
                        <b-icon
                          icon="three-dots"
                          @click="showInfo(true)"
                          aria-hidden="true"
                          class="primary"
                        ></b-icon>
                      </b-col>
                    </b-row>
                  </b-col>
                </b-row>
                <b-row class="desk">
                  <b-col class="col-2">
                    <b-avatar
                      variant="primary"
                      src="https://i.pinimg.com/originals/ee/bb/d0/eebbd0baab26157ff9389d75ae1fabb5.jpg"
                      size="60"
                    ></b-avatar>
                  </b-col>
                  <b-col class="detail">
                    <h5>Louis Litt</h5>
                    <p>Online</p>
                  </b-col>
                  <b-col class="col-4">
                    <b-row class="mt-3 ml-5">
                      <b-col class="col-3">
                        <b-icon
                          class="msg-icon primary icon-size"
                          icon="search"
                        ></b-icon>
                      </b-col>

                      <b-col>
                        <b-dropdown
                          id="dropdown-1"
                          class=" mt-md-0 drop-hover"
                          no-caret
                          dropleft
                          variant="outline-light"
                        >
                          <template #button-content>
                            <b-icon-three-dots
                              class="primary"
                            ></b-icon-three-dots>
                          </template>

                          <b-dropdown-item-button @click="showInfo(true)">
                            View Profile
                          </b-dropdown-item-button>

                          <b-dropdown-item-button>
                            Disable Notification
                          </b-dropdown-item-button>

                          <b-dropdown-item-button>
                            Delete Contact
                          </b-dropdown-item-button>

                          <b-dropdown-item-button>
                            Delete Chat
                          </b-dropdown-item-button>
                        </b-dropdown>
                      </b-col>
                    </b-row>
                  </b-col>
                </b-row>
              </div>

              <section
                class="chats"
                style="
             margin-left: 1px;"
              >
                <div v-for="chat in chats" :key="chat.id">
                  <div v-if="chat.type == 'received'" id="received">
                    <b-row class="p-4">
                      <b-avatar
                        variant="primary"
                        src="https://i.pinimg.com/originals/ee/bb/d0/eebbd0baab26157ff9389d75ae1fabb5.jpg"
                      ></b-avatar>
                      <b-col>
                        <p>
                          <span class="name"> {{ chat.name }} </span>
                        </p>
                        <p class="msg-text mt-0 text">
                          {{ chat.message }}
                          <span class="float-right mt-2 white ">
                            {{ chat.timeStamp }}
                          </span>
                        </p>
                      </b-col>
                    </b-row>
                  </div>
                  <div v-if="chat.type == 'sent'">
                    <b-row class="p-4">
                      <b-col>
                        <p class="sent-name">
                          <span class="name">{{ chat.name }}</span>
                        </p>
                        <p id="sent" class="msg-text-sent text">
                          {{ chat.message }}
                          <span class="float-right mt-2 white">
                            {{ chat.timeStamp }}
                          </span>
                        </p>
                      </b-col>
                      <b-avatar
                        variant="primary"
                        src="https://i.pinimg.com/originals/ee/bb/d0/eebbd0baab26157ff9389d75ae1fabb5.jpg"
                      ></b-avatar>
                    </b-row>
                  </div>
                </div>
              </section>
              <div class="bottom ">
                <b-row v-if="!checked">
                  <b-col cols="2" class="p-0">
                    <b-icon
                      class="msg-icon primary icon-size  icon-top float-right text-right"
                      icon="paperclip"
                    ></b-icon>
                  </b-col>
                  <b-col cols="8" class="p-0">
                    <b-form-input
                      id="textarea"
                      v-model="input"
                      class="input-background"
                      placeholder="Enter something..."
                    ></b-form-input>

                    <div class="wrapper">
                      <emoji-picker @emoji="append" :search="search">
                        <div
                          class="emoji-invoker"
                          slot="emoji-invoker"
                          slot-scope="{ events: { click: clickEvent } }"
                          @click.stop="clickEvent"
                        >
                          <svg
                            height="24"
                            viewBox="0 0 24 24"
                            width="24"
                            class="svgg"
                            xmlns="http://www.w3.org/2000/svg"
                          >
                            <path d="M0 0h24v24H0z" fill="none" />
                            <path
                              d="M11.99 2C6.47 2 2 6.48 2 12s4.47 10 9.99 10C17.52 22 22 17.52 22 12S17.52 2 11.99 2zM12 20c-4.42 0-8-3.58-8-8s3.58-8 8-8 8 3.58 8 8-3.58 8-8 8zm3.5-9c.83 0 1.5-.67 1.5-1.5S16.33 8 15.5 8 14 8.67 14 9.5s.67 1.5 1.5 1.5zm-7 0c.83 0 1.5-.67 1.5-1.5S9.33 8 8.5 8 7 8.67 7 9.5 7.67 11 8.5 11zm3.5 6.5c2.33 0 4.31-1.46 5.11-3.5H6.89c.8 2.04 2.78 3.5 5.11 3.5z"
                            />
                          </svg>
                        </div>
                        <div
                          slot="emoji-picker"
                          slot-scope="{ emojis, insert, display }"
                        >
                          <div
                            class="emoji-picker"
                            :style="{
                              top: display.y + 'px',
                              left: display.x + 'px'
                            }"
                          >
                            <div class="emoji-picker__search">
                              <input type="text" v-model="search" v-focus />
                            </div>
                            <div>
                              <div
                                v-for="(emojiGroup, category) in emojis"
                                :key="category"
                              >
                                <h5>{{ category }}</h5>
                                <div class="emojis">
                                  <span
                                    v-for="(emoji, emojiName) in emojiGroup"
                                    :key="emojiName"
                                    @click="insert(emoji)"
                                    :title="emojiName"
                                    >{{ emoji }}</span
                                  >
                                </div>
                              </div>
                            </div>
                          </div>
                        </div>
                      </emoji-picker>
                    </div>
                  </b-col>

                  <b-col cols="2" class="p-0">
                    <b-icon
                      @click="send"
                      class="msg-icon primary icon-size icon-top "
                      icon="cursor-fill"
                    ></b-icon>
                  </b-col>
                </b-row>
                <p v-if="checked" class="ml-5">
                  You have blocked messages and calls from this user.
                  <b-link @click="showInfo(true)">Unblock Now</b-link>
                </p>
              </div>
            </div>
          </b-col>

          <b-col v-if="info">
            <div class="info-nav">
              <b-button class="primary-bg" @click="showInfo(false)">
                <fas-icon :icon="['fas', 'arrow-left']" />
              </b-button>
              <span class="cnt-info"> Contact Info</span>
            </div>
            <div class="info-bottom">
              <b-avatar
                class="info-avatar"
                variant="primary"
                src="https://i.pinimg.com/originals/ee/bb/d0/eebbd0baab26157ff9389d75ae1fabb5.jpg"
                size="200"
              ></b-avatar>
              <div class="info-detail">
                <h1 class="info-name">Louis Litt</h1>
                <b-link class="primary">View Profile</b-link>
              </div>
            </div>
            <div>
              <ul>
                <li>Options</li>
                <li>
                  <b-row
                    ><b-col>
                      Block Messages
                    </b-col>
                    <b-col>
                      <b-form-checkbox
                        v-model="checked"
                        name="check-button"
                        class="primary"
                        switch
                      >
                      </b-form-checkbox>
                    </b-col>
                  </b-row>
                </li>
                <li>Report User</li>
              </ul>
            </div>
          </b-col>
          <b-col
            v-if="newMsg == true && info == false"
            class="p-0 col-xl-8 col-12"
          >
            <div class="new-msg back-image" style="margin-right: 17px;">
              <div class="info-nav">
                <b-row>
                  <b-col class="col-1 mt-3">
                    To
                  </b-col>
                  <b-col>
                    <b-form-input
                      id="textarea"
                      v-model="searchQuery"
                      class="input-background"
                      style="width: 100%"
                      placeholder="Type the name of person or Business..."
                      @click="showsearchh()"
                    ></b-form-input>

                    <br />

                    <div class="table-responsive" v-if="showsearch == true">
                      <table v-if="resources.length" class="table">
                        <thead>
                          <tr></tr>
                        </thead>
                        <tbody>
                          <tr
                            v-for="item in resultQuery"
                            :key="item.key"
                            class="p-2 message"
                            @click="showInfo(false)"
                          >
                            <td>
                              <b-avatar
                                class="d-inline-block "
                                variant="primary"
                                size="30"
                                v-bind:src="item.profile"
                              ></b-avatar>
                              <span class="bold"> {{ item.name }} </span>
                            </td>
                          </tr>
                        </tbody>
                      </table>
                    </div>
                  </b-col>
                </b-row>
              </div>

              <div class="bottom newMsg-bottom">
                <b-row>
                  <b-col cols="2" class="p-0">
                    <b-icon
                      class="msg-icon primary icon-size     icon-top float-right text-right"
                      icon="paperclip"
                    ></b-icon>
                  </b-col>
                  <b-col cols="8" class="p-0">
                    <b-form-input
                      id="textarea"
                      v-model="text"
                      class="input-background"
                      placeholder="Enter something..."
                    ></b-form-input>
                  </b-col>

                  <b-col cols="2" class="p-0">
                    <b-icon
                      @click="send"
                      class="msg-icon primary icon-size icon-top "
                      icon="cursor-fill"
                    ></b-icon>
                  </b-col>
                </b-row>
              </div>
            </div>
          </b-col>
        </b-row>
      </div>
        <!-- start static messages -->
      <div class="controls field has-addons">
          <div class="control is-expanded">
              <input v-model="message" v-on:keydown.enter="send" class="input is-primary" placeholder="Write message">
          </div>
          <div class="control">
              <button v-on:click="send" :disabled="!message" class="button is-primary">Send</button>
          </div>
      </div>              
      <div class="media-content">
          <div class="content">
              <p>
                  <strong>{{messageData.user}}</strong> <small>{{messageData.date}}</small>
                  <br>
                  {{messageData.text}}
              </p>
          </div>
      </div>
      <div id="nameInput" v-show="!isLogged">
                        <div class="field is-grouped">
                            <div class="control">
                                <input v-model="userName" v-on:keydown.enter="sendUserName" class="input is-primary" placeholder="Your name">
                            </div>
                            <div class="control">
                                <button v-on:click="sendUserName" :disabled="!userName" class="button is-primary">Enter</button>
                            </div>
                        </div>
                    </div>
    </b-container>
    <Footer />




  </div>
</template>

<script>

import Navbar from "@/components/navbar";
import Footer from "@/components/footer";
import EmojiPicker from "vue-emoji-picker";
import { io } from "socket.io-client";
const socket = io();

export default {
  sockets:{
    connect: function(){
      console.log('socket connected')
    },
    customEmit: function(val){
      console.log('this method fired by socket server. eg: io.emit("customEmit", data)')
    }
  },
  components: {
    Navbar,
    Footer,
    EmojiPicker
  },
  data() {
    return {
      input: "",
      search: "",
      messageData:'',
      messages: [],
      users: [],
      userName: '',
      isLogged: false,
      showsearch: true,
      selecteduser: false,

      searchQuery: null,
      resources1: [
        { title: "ABE Attendance", uri: "aaaa.com", category: "a", icon: null },
        {
          title: "Accounting Services",
          uri: "aaaa.com",
          category: "a",
          icon: null
        },
        { title: "Administration", uri: "aaaa.com", category: "a", icon: null },
        {
          title: "Advanced Student Lookup",
          uri: "bbbb.com",
          category: "b",
          icon: null
        },
        { title: "Art & Sciences", uri: "bbbb.com", category: "b", icon: null },
        {
          title: "Auxiliares Services",
          uri: "bbbb.com",
          category: "b",
          icon: null
        },
        { title: "Basic Skills", uri: "cccc.com", category: "c", icon: null },
        {
          title: "Board of Trustees",
          uri: "dddd.com",
          category: "d",
          icon: null
        }
      ],
      resources: [
        {
          name: "blezour blec",
          profile:
            "https://i.pinimg.com/originals/ee/bb/d0/eebbd0baab26157ff9389d75ae1fabb5.jpg",
          type: "person",
          id: "1"
        },
        {
          name: "itz blec blec",
          profile:
            "https://i.pinimg.com/originals/ee/bb/d0/eebbd0baab26157ff9389d75ae1fabb5.jpg",
          type: "person",
          id: "2"
        },

        {
          name: "Maxine Moffet",
          profile:
            "https://i.pinimg.com/originals/ee/bb/d0/eebbd0baab26157ff9389d75ae1fabb5.jpg",
          type: "person",
          id: "3"
        },

        {
          name: "Alicia kays",
          profile:
            "https://i.pinimg.com/originals/ee/bb/d0/eebbd0baab26157ff9389d75ae1fabb5.jpg",
          type: "person",
          id: "4"
        },

        {
          name: "Lorem Ipsum",
          profile:
            "https://i.pinimg.com/originals/ee/bb/d0/eebbd0baab26157ff9389d75ae1fabb5.jpg",
          type: "person",
          id: "5"
        },
        {
          name: "blezour blec",
          profile:
            "https://i.pinimg.com/originals/ee/bb/d0/eebbd0baab26157ff9389d75ae1fabb5.jpg",
          type: "person",
          id: "6"
        }
      ],
      message: {
        type: "",
        name: "Louis Litt",
        timeStamp: "",
        message: ""
      },
      newMsg: false,
      show: false,
      info: false,
      checked: false,
      text: "",
      selected: [],
      chats: [
        {
          id: 0,
          type: "received",
          name: "Louis Litt",
          timeStamp: "3:00 PM",

          message:
            "Lorem ipsum dolor sit, amet consectetur adipisicing elit. Explicabo, quos? Fuga, nam dolores? Tempora, qui."
        },
        {
          id: 1,
          type: "sent",
          name: "Louis Litt",
          timeStamp: "3:00 PM",
          message:
            "Lorem ipsum dolor sit, amet consectetur adipisicing elit. Explicabo, quos? Fuga, nam dolores? Tempora, qui."
        },
        {
          id: 2,
          type: "received",
          name: "Louis Litt",
          timeStamp: "3:00 PM",
          message:
            "Lorem ipsum dolor sit, amet consectetur adipisicing elit. Explicabo, quos? Fuga, nam dolores? Tempora, qui."
        },
        {
          id: 3,
          type: "sent",
          name: "Louis Litt",
          timeStamp: "3:00 PM",
          message:
            "Lorem ipsum dolor sit, amet consectetur adipisicing elit. Explicabo, quos? Fuga, nam dolores? Tempora, qui."
        },
        {
          id: 4,
          type: "received",
          name: "Louis Litt",
          timeStamp: "3:00 PM",
          message:
            "Lorem ipsum dolor sit, amet consectetur adipisicing elit. Explicabo, quos? Fuga, nam dolores? Tempora, qui."
        },
        {
          id: 5,
          type: "sent",
          name: "Louis Litt",
          timeStamp: "3:00 PM",
          message:
            "Lorem ipsum dolor sit, amet consectetur adipisicing elit. Explicabo, quos? Fuga, nam dolores? Tempora, qui."
        }
      ],
      // messages: [
      //   {
      //     id: 0,
      //     name: "Blezour blec",
      //     startMessage: "Hello Blec lola blec ",
      //     timeStamp: "3:00pm",
      //     messageCount: "10"
      //   },
      //   {
      //     id: 1,
      //     name: "Blec blezour blec",
      //     startMessage: "yoo nigga sup lola blec",
      //     timeStamp: "7:00am",
      //     messageCount: "60"
      //   },

      //   {
      //     id: 3,
      //     name: "baba blecc ",
      //     startMessage: "Lorem ipsum la lola blec vlr ",
      //     timeStamp: "9:00am",
      //     messageCount: "60"
      //   },
      //   {
      //     id: 4,
      //     name: "Louis Litt",
      //     startMessage: "Lorem  sit amet this is goo.",
      //     timeStamp: "6:00am",
      //     messageCount: "6"
      //   },
      //   {
      //     id: 5,
      //     name: "Louis Litt",
      //     startMessage: "Lorem this   sit amet.",
      //     timeStamp: "7:00am",
      //     messageCount: "100"
      //   },
      //   {
      //     id: 6,
      //     name: "Louis Litt",
      //     startMessage: "Lorem ithe amet.",
      //     timeStamp: "7:00am",
      //     messageCount: "3"
      //   },
      //   {
      //     id: 7,
      //     name: "Louis Litt",
      //     startMessage: "Lordol sit amet.",
      //     timeStamp: "7:00am",
      //     messageCount: "10"
      //   },
      //   {
      //     id: 8,
      //     name: "Louis Litt",
      //     startMessage: "Lorem vheck ",
      //     timeStamp: "7:00am",
      //     messageCount: "40"
      //   },
      //   {
      //     id: 9,
      //     name: "Louis Litt",
      //     startMessage: "Lorem papa .",
      //     timeStamp: "7:00am",
      //     messageCount: "15"
      //   }
      // ]
    };
  },

  directives: {
    focus: {
      inserted(el) {
        el.focus();
      }
    }
  },
  created() {
           
           socket.on("sendMessage", () => {
                console.log('connection------',socket.id); // x8WIv7-mJelg7on_ALbx
              });
  },
   watch: {
            newMessage(value) {
                value ? socket.emit('typing', this.username) : socket.emit('stopTyping')
            }
        },

  methods: {
    //  sendMessage: function(message) {
    //    console.log('function call-------',message);
    //     if (message) {
    //       socket.emit('send-msg', { message: message, user: this.userName });
    //     }
    //   },
      setName: function(userName) {
        this.userName = userName;
        this.isLogged = true;
        socket.emit('add-user', this.userName);
      },
      scrollToEnd: function() {
        var container = this.$el.querySelector('.messages');
        console.log(container);
        console.log(this.$el);
        container.scrollTop = container.scrollHeight;
      },
    sendUserName: function() {
        if (this.userName.length > 0) {
          this.$emit('set-name', this.userName);
        }
      },
     send: function() {
       let that=this;
        if (that.message.length > 0) {
          console.log('send function call------',that.message);
          that.$emit('sendMessage', that.message);
          that.message = '';
        }
      },
    insert(emoji) {
      this.input += emoji;
    },

    append(emoji) {
      this.input += emoji;
    },

    selectuser() {
      this.showsearch = false;

      this.selecteduser = true;
    },

    showsearchh() {
      this.showsearch = true;
    },

    showMessages(arg) {
      this.show = arg;
    },
    showInfo(arg) {
      this.info = arg;
      this.newMsg = arg;
      console.log(this.checked);
    },
    newMessage(arg) {
      console.log("hey");
      this.newMsg = arg;
      this.show = false;
    },
    // send() {
    //   this.message.type = "sent";
    //   let today = new Date();
    //   let h = today.getHours();
    //   let m = today.getMinutes();
    //   this.message.timeStamp = h + ":" + m;
    //   this.message.message = this.text;
    //   this.chats.push(this.message);
    //   this.text = "";
    // }
  },

  computed: {
    resultQuery() {
      if (this.searchQuery) {
        return this.resources.filter(item => {
          return this.searchQuery
            .toLowerCase()
            .split(" ")
            .every(v => item.name.toLowerCase().includes(v));
        });
      } else {
        return this.resources;
      }
    }
  }
};



</script>

<style scoped>
.right {
  padding: 10px;
  border-right: 2px solid #ccc;
}
.primary-bg,
.primary-bg:hover {
  background-color: #e75c18;
  border: none;
}

.chat-box {
  position: relative;

  border: solid 2px rgb(223, 223, 223);
  margin-bottom: 100px;
}

.chat-nav {
  position: relative;
  min-height: 70px;
  border-right: 2px solid #ccc;

  width: 100%;

  padding: 10px;
}
.chats {
  height: 710px;
  overflow-y: scroll;
  overflow-x: hidden;
}

.back-image {
  background-image: url("../assets/message_back.jpg");
  background-repeat: no-repeat;
  background-size: cover;
}
input {
  margin-top: 10px;
}
h1 {
  margin-top: 20px;
}
.new-message {
  margin-top: 20px;
  cursor: pointer;
}

.messages {
  overflow-y: scroll;
  overflow-x: hidden;
  height: 710px;
}
.txt {
  font-size: 13px;
}
.message {
  cursor: pointer;
}
.message:hover {
  background-color: #e75d29;
  color: #fff;
}

.msg-icon {
  font-size: 20px;
  cursor: pointer;
}

.icons {
  margin-left: -60px;
  margin-top: 10px;
}
.msg-text {
  width: 60%;
  border-radius: 25px;
  color: #fff;
  background-color: #ed9970;
  padding: 10px;
  font-size: 12px;
}
.msg-text-sent {
  position: relative;
  min-width: 60%;
  border-radius: 25px;
  background-color: #bfbfbf;
  padding: 10px;
  font-size: 12px;
}
.name {
  font-weight: bold;
}

#sent {
  margin-left: 200px;
}
.sent-name {
  margin-left: 400px;
}
.bottom {
  padding-left: 10px;

  height: 60px;

  border-bottom-right-radius: 15px;
  background-color: white;
}
.detail {
  margin-left: -40px;
}

.mobile {
  display: none;
}

.right-mobile {
  display: none;
}

.info-nav {
  position: relative;
  min-height: 70px;
  height: 70px;
  width: 100%;
  padding: 10px;
}
.cnt-info {
  margin-left: 130px;
  font-weight: bold;
  font-size: 20px;
}
.info-bottom {
  padding: 20px;
  border-bottom: 1px solid #ccc;
}
.info-avatar {
  margin-left: 150px;
}
.info-detail {
  text-align: center;
}
li {
  list-style: none;
  margin-top: 10px;
}
#text-area {
  width: 100%;
}
.newMsg-bottom {
  margin-top: 717px;
}
.new-msg {
  background-color: #ccc;
}
@media only screen and (max-width: 768px) {
  .m-10 {
    margin-top: 10px;
  }
  .mobile {
    display: flex;
  }
  .right {
    display: none;
  }
  .messages {
    display: none;
  }
  .chat-nav {
    position: relative;
    min-height: 70px;

    width: 100%;
    padding: 10px;
    border-right: none;
    padding: 10px;
    border-top-right-radius: 20px;
    border-top-left-radius: 20px;
    margin-top: -3px;
  }
  .desk {
    display: none;
  }

  #sent {
    margin-left: 100px;
  }
  .sent-name {
    margin-left: 10px;
  }
  h5 {
    font-size: 10px;
  }
  .user {
    display: none;
  }
  #textarea {
    margin-left: 0px;

    margin-top: 5px;
    margin-bottom: 5px;
  }
  .msg-icon {
    font-size: 20px;
    cursor: pointer;
  }

  .icons {
    margin-left: -90px;
    margin-top: 10px;
  }
  .detale {
    margin-left: -18px;
  }
  .right-mobile {
    display: block;
    padding: 10px;
  }
  .messages-mobile {
    overflow-y: scroll;
    overflow-x: hidden;
    height: 690px;
    border-top: none;
    overflow-x: hidden;
    width: 97%;
  }
  .message {
    cursor: pointer;
    width: 100%;
  }
  h1 {
    font-size: 25px;
  }
  .info-nav {
    position: relative;
    min-height: 70px;
    height: 70px;
    width: 100%;
    padding: 10px;
  }

  .info-bottom {
    padding: 20px;
    border-bottom: 1px solid #ccc;
  }
  .info-avatar {
    margin-left: 40px;
  }
  .info-detail {
    text-align: center;
  }
  li {
    list-style: none;
    margin-top: 10px;
  }
  .info-media {
    padding: 10px;
  }
  .media {
    display: flex;
    flex-wrap: wrap;
  }
}

::-webkit-scrollbar {
  width: 4px;
}

/* Track */
::-webkit-scrollbar-track {
  background: #f1f1f1;
}

/* Handle */
::-webkit-scrollbar-thumb {
  background: #888;
}

/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
  background: #555;
}

.input-background {
  background-color: #ccc;
  border-radius: 20px;
}

.icon-top {
  margin-top: 14px;
}

.profile-pic {
  width: 64px !important;
  height: 64px !important;
}

.drop-hover:hover {
  background-color: white;
}

.drop-hover:active {
  background-color: white;
}

.drop-hover:hover {
  background-color: white;
}

.duration {
  margin-top: 5px;
}

.wrapper {
  position: relative;
  display: inline-block;
}

.regular-input {
  padding: 0.5rem 1rem;
  border-radius: 3px;
  border: 1px solid #ccc;
  width: 20rem;
  height: 12rem;
  outline: none;
}

.regular-input:focus {
  box-shadow: 0 0 0 3px rgba(66, 153, 225, 0.5);
}

.emoji-invoker {
  position: absolute;
  top: 0.5rem;
  right: 0.5rem;
  width: 1.5rem;
  height: 1.5rem;
  border-radius: 50%;
  cursor: pointer;
  transition: all 0.2s;
}
.emoji-invoker:hover {
  transform: scale(1.1);
}
.emoji-invoker > svg {
  fill: #b1c6d0;
}

.svgg {
  margin-top: -120px;
  margin-left: -20px;
}

.emoji-picker {
  top: -370px !important;
  left: 0px !important;

  position: absolute;
  z-index: 1;
  font-family: Montserrat;
  border: 1px solid #ccc;
  width: 15rem;
  height: 20rem;
  overflow: auto;
  padding: 1rem;
  box-sizing: border-box;
  border-radius: 0.5rem;
  background: #fff;
  box-shadow: 1px 1px 8px #c7dbe6;
}
.emoji-picker__search {
  display: flex;
  overflow-x: hidden;
}
.emoji-picker__search > input {
  flex: 1;
  border-radius: 10rem;
  border: 1px solid #ccc;
  padding: 0.5rem 1rem;
  outline: none;
  height: 32px;

  width: 90%;
}
.emoji-picker h5 {
  margin-bottom: 0;
  color: #b1b1b1;
  text-transform: uppercase;
  font-size: 0.8rem;
  cursor: default;
}
.emoji-picker .emojis {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}
.emoji-picker .emojis:after {
  content: "";
  flex: auto;
}
.emoji-picker .emojis span {
  padding: 0.2rem;
  cursor: pointer;
  border-radius: 5px;
}
.emoji-picker .emojis span:hover {
  background: #ececec;
  cursor: pointer;
}
</style>
