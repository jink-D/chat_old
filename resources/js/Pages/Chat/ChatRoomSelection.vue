<template>
  <div id="chatroom_selector">
    <div class="font-bold text-xl contents">{{ selected.name }} Chat</div>

    <div class="contents">
      <select
        v-model="selected"
        @change="$emit('RoomChanged', selected)"
        class="float-right"
      >
        <option v-for="(room, index) in rooms" :key="index" :value="room">
          {{ room.name }}
        </option>
      </select>
    </div>
  </div>
</template>

<script>
export default {
  props: ["rooms", "currentRoom"],
  data: function () {
    return {
      selected: "",
    };
  },
  created() {
    this.selected = this.currentRoom;
  },
};
</script>

<style>
</style>
