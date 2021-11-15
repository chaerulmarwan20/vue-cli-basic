<template>
  <div id="app" class="container mt-5">
    <h1>ARL Shop</h1>
    <p class="animate__animated animate__fadeInRight">
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Placeat a
      blanditiis ullam sed voluptatibus ea commodi rerum tempore molestiae quam
      optio aut, iure ducimus aperiam qui, voluptate minus similique veritatis.
    </p>
    <font-awesome-icon icon="shopping-cart"></font-awesome-icon>
  </div>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";

export default {
  name: "App",
  components: {
    FontAwesomeIcon,
  },
};
</script>
