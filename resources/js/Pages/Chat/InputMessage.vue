<template>
  <div class="relative m-1">
    <div class="w-full" style="border-top: 1px solid #e6e6e6">
      <textarea
        class="w-full outline-none p-1"
        type="text"
        v-model="message"
        placeholder="メッセージを入力"
        @keyup.enter.ctrl="sendMessage()"
      />
      <div id="send_menu_list" class="relative">
        <div id="send_message_btn" class="text-right">
          <button @click="sendMessage()" style="">
            <img src="/storage/icons/send.jpg" />
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["room"],
  data: function () {
    return {
      message: "",
    };
  },
  methods: {
    sendMessage() {
      if (this.message == "") {
        return;
      } else {
        axios
          .post("/chat/room/" + this.room.id + "/store/message", {
            message: this.message,
          })
          .then((response) => {
            if (response.status == 201) {
              (this.message = ""), this.$emit("MessageSent");
              //   alert("Message Sent");
            }
          })
          .catch((error) => {
            alert("Message Send Error");
          });
      }
    },
  },
};
</script>

<style src="vue2-perfect-scrollbar/dist/vue2-perfect-scrollbar.css"/>
<style>
.ps {
  overflow: hidden;
  height: 100%;
  border: 1px gray;
}
</style>
