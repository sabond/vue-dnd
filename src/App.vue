<template>
  <div id="app">
    <vue-draggable-resizable :w="100" :h="100" @dragstop="onDragStop">
      <p v-if="parentPageNumber">Parent Page: {{ parentPageNumber }}</p>
      <p v-else>No Parent Page</p>
    </vue-draggable-resizable>
    <div class="container">
      <div>Drag top-left corner of box to a page</div>
      <Page page-number="1" /> <Page page-number="2" />
    </div>
  </div>
</template>

<script>
import Page from "./components/Page";

export default {
  name: "App",
  components: {
    Page
  },
  data() {
    return {
      parentPageNumber: null
    };
  },
  methods: {
    onDragStop(x, y) {
      /* For example's sake, this element lookup is simplified in that
          only considers the top-left corner given by `(x,y)`, but
          you might want to evalute additional coordinates e.g., to meet
          a minimum threshold before overlap is verified. */
      const el = document.elementFromPoint(x, y);
      this.parentPageNumber = el.dataset.pageNumber;
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.container {
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  height: 100vh;
}

/* Set pointer-events:none on <vue-draggable-resizable>'s
  draggable element while dragging so that document.elementFromPoint()
  will grab the element underneath */
.dragging {
  pointer-events: none;
}
</style>
