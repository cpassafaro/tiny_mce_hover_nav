<template>
  <div id="app">
    <editor api-key="no-api-key" :init="config" />
  </div>
</template>

<script>
import Editor from "@tinymce/tinymce-vue";

export default {
  name: "app",
  components: {
    editor: Editor,
  },
  props: {
    value: { type: Object, required: false, default: null },
  },
  data() {
    return {
      toolbar:
        "undo redo | formatselect | bold italic backcolor | \
          alignleft aligncenter alignright alignjustify | \
          bullist numlist outdent indent | removeformat | help",
    };
  },
  computed: {
    config() {
      if (this.value) {
        return this.value;
      } else {
        return {
          height: 500,
          toolbar: this.toolbar,
          plugins: [
            "advlist autolink lists link image charmap print preview anchor",
            "searchreplace visualblocks code fullscreen",
            "insertdatetime media table paste code help wordcount",
          ],
          menubar: false,
        };
      }
    },
  },
};
</script>
