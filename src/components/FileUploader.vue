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
      if (!file) return;

      const reader = new FileReader();
      reader.onload = (event) => {
        try {
          const data = JSON.parse(event.target.result);

          if (this.isArrayofObjects(data)) {
            this.$emit("file-loaded", data);
          } else {
            alert("Invalid JSON structure. Expected an array of objects.");
          }
        } catch (error) {
          alert("Failed to load file. Please ensure it is a valid JSON.");
        }
      };
      reader.readAsText(file);
    },
    isArrayofObjects(data) {
      return (
        Array.isArray(data) &&
        data.every(
          (item) =>
            typeof item === "object" && item !== null && !Array.isArray(item)
        )
      );
    }
  }
};
</script>
