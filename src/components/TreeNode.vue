<template>
  <li>
    <div class="node">
      {{ node.id }}
      <div class="buttons">
        <button @click="addChild">Add</button>
        <button @click="removeNode">Delete</button>
      </div>
    </div>
    <ul v-if="children.length">
      <tree-node
        v-for="child in children"
        :key="child.id"
        :node="child"
        @add-node="$emit('add-node', $event)"
        @delete-node="$emit('delete-node', $event)"
      ></tree-node>
    </ul>
  </li>
</template>

<script>
export default {
  name: "TreeNode",
  props: {
    node: {
      type: Object,
      required: true
    }
  },
  computed: {
    children() {
      return this.$root.nodes.filter((n) => n.parent_id === this.node.id);
    }
  },
  methods: {
    addChild() {
      this.$emit("add-node", this.node.id);
    },
    removeNode() {
      this.$emit("delete-node", this.node.id);
    }
  }
};
</script>
