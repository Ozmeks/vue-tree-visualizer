<template>
  <div>
    <input type="file" @change="loadFile" />
  </div>
</template>

<script>
export default {
  methods: {
    loadFile(event) {
      const file = event.target.files[0];
      const reader = new FileReader();
      reader.onload = (event) => {
        this.$emit("file-loaded", JSON.parse(event.target.result));
      };
      reader.readAsText(file);
    }
  }
};
</script>
