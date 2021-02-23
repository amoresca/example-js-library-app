<template>
  <div class="home">
    <header>Cool Header</header>
    <section>
      <h1>Section 1</h1>
    </section>
    <section>
      <h1>Section 2</h1>
      <button v-on:click="pinHeader()">Bring Back Header</button
      ><button v-on:click="unpinHeader()">Hide Header</button>
    </section>
    <section>
      <h1>Section 3</h1>
    </section>
  </div>
</template>

<style>
body {
  margin: 0;
  padding: 0;
  text-align: left;
}
header {
  position: fixed;
  top: 0;
  width: 100%;
  padding: 1em 0;
  background-color: rgb(121, 69, 121);
  color: white;
  font-size: 2em;
  text-align: center;
}
.headroom {
  will-change: transform;
  transition: transform 200ms linear;
}
.headroom--pinned {
  transform: translateY(0%);
}
.headroom--unpinned {
  transform: translateY(-100%);
}
section {
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

section:nth-child(even) {
  background-color: #e4dae4;
}
.state {
  position: fixed;
  bottom: 0;
  left: 1em;
}
</style>

<script>
import Headroom from "headroom.js";

export default {
  data: function() {
    return {
      headroom: "",
    };
  },
  methods: {
    pinHeader: function() {
      this.headroom.pin();
    },
    unpinHeader: function() {
      this.headroom.unpin();
    },
  },
  mounted: function() {
    // grab an element
    var myElement = document.querySelector("header");
    var options = {
      tolerance: 10,
    };
    // construct an instance of Headroom, passing the element
    this.headroom = new Headroom(myElement, options);
    // initialise
    this.headroom.init();
  },
};
</script>
