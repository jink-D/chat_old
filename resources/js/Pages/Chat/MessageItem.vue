<template>
  <div id="message_container">
    <!-- <div id="message_action" class="text-right">
      <button id="message_delete" v-on:click="editMessage(message.id)">
        <img src="/storage/icons/edit.jpg" />
      </button>
      <button id="message_delete" v-on:click="deleteMessage(message.id)">
        <img src="/storage/icons/trashbox.jpg" />
      </button>
    </div> -->
    
    <div id="user_photo" class="inline-flex rounded-md">
      <button
        class="
          flex
          text-sm
          border-2 border-transparent
          rounded-full
          focus:outline-none
          focus:border-gray-300
          transition
          duration-150
          ease-in-out
        "
      >
        <img
          v-if="$page.props.jetstream.managesProfilePhotos"
          class="h-8 w-8 rounded-full object-cover"
          :src="message.user.profile_photo_url"
          :alt="message.user.name"
        />
      </button>
    </div>
    <div id="user_name" class="inline-flex" style="position: absolute">
      <b>{{ message.user.name }}</b> &nbsp;
      <div id="message_created_at" class="contents" style="font-size: 8px">
        {{ message.created_at | moment("YYYY/MM/DD HH:mm") }}
      </div>
    </div>
    <div id="message_contents" class="inline-flex" style="position: relative">
      {{ message.message }}
    </div>
  </div>
</template>

<script>
export default {
  props: ["currentRoom", "message"],
  methods: {
    // editMessage(message_id) {
    //   //
    // },
    // deleteMessage(message_id) {
    //   axios
    //     .post(`chat/room/${this.currentRoom.id}/delete/message${message_id}`)
    //     .then((response) => {
    //       return;
    //     })
    //     .catch((error) => {
    //       alert("Message delete failed");
    //     });
    // },
  },
};
</script>

<style>
</style>
