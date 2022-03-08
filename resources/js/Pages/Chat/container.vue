<template>
  <app-layout>
    <template #header>
      <h2 class="font-semibold text-xl text-gray-800 leading-tight">
        <chat-room-selection
          v-if="currentRoom.id"
          :rooms="chatRooms"
          :currentRoom="currentRoom"
          v-on:RoomChanged="setRoom($event)"
        />
      </h2>
    </template>

    <div class="py-12">
      <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
        <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg">
          <messages-container :messages="messages" />
          <input-message :room="currentRoom" v-on:MessageSent="getMessages()" />
        </div>
      </div>
    </div>
  </app-layout>
</template>

<script>
import AppLayout from "@/Layouts/AppLayout";
import MessagesContainer from "./MessagesContainer.vue";
import InputMessage from "./InputMessage.vue";
import ChatRoomSelection from "./ChatRoomSelection.vue";

export default {
  components: {
    AppLayout,
    MessagesContainer,
    InputMessage,
    ChatRoomSelection,
  },
  data: function () {
    return {
      chatRooms: [],
      currentRoom: [],
      messages: [],
    };
  },
  watch: {
    currentRoom(newVal, oldVal) {
      if (oldVal.id) {
        this.disconnect(oldVal);
      }
      this.connect();
    },
  },
  methods: {
    connect() {
      this.getMessages();
      window.Echo.private("laravel-chat." + this.currentRoom.id).listen(
        "NewChatMessage",
        (e) => {
          this.getMessages();
        }
      );
    },
    disconnect(room) {
      window.Echo.leave("laravel-chat." + room.id);
    },
    getRooms() {
      axios
        .get("/chat/rooms")
        .then((response) => {
          this.chatRooms = response.data;
          this.setRoom(response.data[0]);
        })
        .catch((error) => {
          alert("getRoom function Error");
        });
    },
    setRoom(room) {
      this.currentRoom = room;
    },
    getMessages() {
      axios
        .get("/chat/room/" + this.currentRoom.id + "/show/messages")
        .then((response) => {
          this.messages = response.data;
        })
        .catch((error) => {
          alert("getMessages function Error");
        });
    },
  },
  mounted() {
    this.getRooms();
  },
};
</script>
