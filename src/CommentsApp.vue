<template>
  <main class="p-4 bg-gray-50 min-h-screen">
    <div class="max-w-screen-xl mx-auto bg-white p-8 rounded-lg shadow-2xl">
      <h2 class="text-3xl my-6">评论</h2>
      <CommentBox @submit="addNewComment" />
      <DividerHorizontal />
      <div
        v-for="comment in comments"
        :key="comment.id"
      >
        <CommentItem 
          :user="comment.user"
          :avatar="comment.avatar"
          :time="comment.time"
          :content="comment.content"
        />
        <ReplyContainer v-if="comment.replies">
          <CommentItem
            v-for="reply in comment.replies"
            :key="reply.id"
            :user="reply.user"
            :avatar="reply.avatar"
            :time="reply.time"
            :content="reply.content"
          />
        </ReplyContainer>
        <reply-box @submit="addNewComment($event, comment.id)" />
      </div>
    </div>
  </main>
</template>

<script setup>
import CommentBox from './components/CommentBox.vue';
import DividerHorizontal from './components/DividerHorizontal.vue';
import CommentItem from './components/CommentItem.vue';
import ReplyBox from './components/ReplyBox.vue';
import ReplyContainer from './components/ReplyContainer.vue';

import face from './assets/wechattemp.png';
import { ref } from '@vue/reactivity';
import { onMounted } from '@vue/runtime-core';

let rid = ref(4);

const comments = ref([]);

async function getAllComments() {
  const res = await fetch("/api/comments");
  comments.value = await res.json();
}

onMounted(() => {
  getAllComments();
})

const addNewComment = async (content, replyTo) => {
 const res = await fetch("/api/comments", { 
    method: "post",

    headers: {
      "content-type": "application/json"
    },
    body: JSON.stringify({
      content: content,
      ...(replyTo && { replyTo })
    })
  })
  
  const newComment = await res.json();
  if(!replyTo) {
    comments.value.unshift(newComment);
  } else {
    comments.value.find(c => c.id === replyTo).replies.unshift(newComment);
  }
}

</script>

<style scoped>

</style>