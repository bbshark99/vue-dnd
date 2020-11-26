<template>
  <div id="app">
    <div class="dropzone">
      <Container 
        group-name="group-1" 
        @drop="onDropItem"
      >
        <div 
          class="drop-item"
          v-for="(item, itemIdx) in items"
          v-bind:key="itemIdx"
        >
          <h5>{{ item }}</h5>
        </div>

        <h3>Drop Here</h3>
      </Container>
    </div>
    <div class="dragzone">
      <Container
        group-name="group-1"
        behaviour="copy"
        :get-child-payload="getChildPayload"
      >
        <Draggable 
          v-for="(library, libraryIdx) in libraries" 
          v-bind:key="libraryIdx"
        >
          <div class="dragger">
            <h5>{{ library }}</h5>
          </div>
        </Draggable>
      </Container>
    </div>
  </div>
</template>

<script>
import { Container, Draggable } from 'vue-smooth-dnd'

export default {
  name: 'App',
  components: {
    Container,
    Draggable
  }, 
  data() {
    return {
      libraries: [
        'Drag me - 1',
        'Drag me - 2',
        'Drag me - 3',
        'Drag me - 4',
        'Drag me - 5',
      ],
      items: []
    }
  },
  methods: {
    onDropItem(dropResult) {
      const { addedIndex: index } = dropResult;
      this.items.splice(index, 0, dropResult.payload);
    },
    getChildPayload(index) {
      return this.libraries[index];
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;

  display: grid;
  grid-template-columns: 65% auto;
}

.dropzone {
  margin: .25rem;
  border: 1px dashed grey;

  min-height: 100px;
}

.dropzone .smooth-dnd-container {
  height: 100%;
}

.dragzone .dragger, .dropzone .drop-item {
  border: 1px solid grey;
  padding: .25rem;
  margin: .25rem;
}
</style>
