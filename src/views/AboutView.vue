<script setup lang="ts">
import { ref } from 'vue'
import SelectCom1 from '../components/SelectCom1.vue'
import SelectCom2 from '../components/SelectCom2.vue'
import Posts from '../components/Posts.vue'
import Post from '../components/Post.vue'

const visitedPosts = ref(new Set())
const isVisited = (id: number) => visitedPosts.value.has(id)

const postId = ref(-1)
const setPostId = (id: number) => {
  visitedPosts.value.add(id)
  postId.value = id
}
</script>
<template>
  <div class="about">
    <h1>Vue Query - Basic</h1>
    <p>
      As you visit the posts below, you will notice them in a loading state the first time you load
      them. However, after you return to this list and click on any posts you have already visited
      again, you will see them load instantly and background refresh right before your eyes!
      <strong>
        (You may need to throttle your network speed to simulate longer loading sequences)
      </strong>
    </p>
    <p>
      當您訪問下面的帖子時，您會注意到它們在第一次加載時處於加載狀態。但是，當您返回此列表並再次單擊您已經訪問過的任何帖子後，您將看到它們立即加載並在您眼前刷新背景！
      （您可能需要限製網路速度來模擬更長的載入序列
    </p>
    <SelectCom1 />
    <SelectCom2 />
    <!-- <h1>This is an about page</h1> -->
    <Post v-if="postId > -1" :postId="postId" @setPostId="setPostId" />
    <Posts v-else :isVisited="isVisited" @setPostId="setPostId" />
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    /* display: flex; */
    align-items: center;
  }
}
</style>
