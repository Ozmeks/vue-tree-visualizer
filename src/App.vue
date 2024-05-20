<template>
  <div id="app">
    <h1>Vue Tree Editor</h1>
    <FileUploader @file-loaded="loadTree" />
    <div class="tree-container">
      <ul>
        <tree-node
          v-for="node in rootNodes"
          :key="node.id"
          :node="node"
          @add-node="addNode"
          @delete-node="deleteNode"
        ></tree-node>
      </ul>
    </div>
  </div>
</template>

<script>
import TreeNode from "./components/TreeNode.vue";
import FileUploader from "./components/FileUploader.vue";

export default {
  components: {
    TreeNode,
    FileUploader
  },
  data() {
    return {
      nodes: []
    };
  },
  computed: {
    rootNodes() {
      return this.nodes.filter((node) => !node.parent_id);
    }
  },
  methods: {
    loadTree(data) {
      this.nodes = data;
    },
    addNode(parentId) {
      const newId = prompt("Enter node ID");

      if (newId === null) {
        // User pressed cancel
        return;
      }

      if (newId.trim() === "") {
        alert("Node ID cannot be empty.");
        return;
      }

      const isExisted = this.nodes.some((node) => node.id === newId);
      if (isExisted) {
        alert("Node ID must be unique.");
      } else {
        this.nodes.push({ id: newId, parent_id: parentId });
      }
    },
    deleteNode(nodeId) {
      const deleteChildren = (id) => {
        this.nodes = this.nodes.filter((node) => node.id !== id);
        this.nodes.forEach((node) => {
          if (node.parent_id === id) deleteChildren(node.id);
        });
      };
      deleteChildren(nodeId);
    }
  }
};
</script>

<style src="./app.css"></style>
