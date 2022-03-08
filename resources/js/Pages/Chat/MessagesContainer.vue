<template>
  <div id="messages_view">
    <div class="w-full p-2 relative flex-col-reverse" style="height: 40rem">
      <perfect-scrollbar>
        <div id="contents">
          <div v-for="(message, index) in messages" :key="index">
            <message-item :message="message" />
          </div>
        </div>
      </perfect-scrollbar>
    </div>
  </div>
</template>

<script>
document.getElementById("contents").scrollIntoView(false);
</script>

<script>
import MessageItem from "./MessageItem.vue";
import { PerfectScrollbar } from "vue2-perfect-scrollbar";
export default {
  components: { MessageItem, PerfectScrollbar },
  props: ["messages"],
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
