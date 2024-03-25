<template>
  <div class="include">
    <editor
      :key="seed"
      api-key="0hpgd4n0xdiraxwsc7gvstlowu1x0rkqvcy8xvktjlyusly8"
      :init="config"
      @onfocus="onEditorFocus"
      v-click-outside="{
        handler: onClickOutside,
        include,
      }"
    />
  </div>
</template>

<script>
import Editor from "@tinymce/tinymce-vue";

export default {
  name: "tinymce-wrapper",
  components: {
    editor: Editor,
  },
  props: {
    value: { type: Object, required: false, default: null },
    height: { type: Number, required: false, default: null },
    menubar: {
      type: String,
      required: false,
      default: "edit insert format  view table windward help",
    },
    toolbar: {
      type: String,
      required: false,
      default:
        "undo redo | formatselect | fontsizeselect  | bold italic underline strikethrough removeformat | alignleft aligncenter alignright | table bullist numlist outdent indent | mathButton ",
    },
  },
  data() {
    return {
      focus: false,
      seed: "",
    };
  },
  computed: {
    filteredMenubar() {
      if (this.focus) {
        return this.menubar;
      } else {
        return "";
      }
    },
    filteredToolbar() {
      if (this.focus) {
        return this.toolbar;
      } else {
        return "";
      }
    },
    filteredHeight() {
      if (!this.focus) {
        return 50;
      } else if (this.height !== null) {
        return this.height;
      } else {
        return 500;
      }
    },
    config() {
      if (this.value) {
        return this.value;
      } else {
        return {
          height: this.filteredHeight,
          visual: false,
          menubar: this.filteredMenubar,
          toolbar: this.filteredToolbar,
          plugins: [
            "advlist autolink lists link image charmap print preview anchor",
            "searchreplace visualblocks code fullscreen",
            "insertdatetime media table paste code help wordcount",
          ],
          table_advtab: false,
          table_cell_advtab: false,
          table_row_advtab: false,
          table_default_attributes: {
            class: "default",
          },
          font_size_formats: "8pt 10pt 12pt 14pt 16pt 18pt 24pt 36pt 48pt",
        };
      }
    },
  },
  methods: {
    onEditorFocus() {
      if (!this.focus) {
        // need to set up crypto key
        this.seed = this.seed + 1;
        this.focus = true;
      }
    },
    onClickOutside() {
      if (this.focus) {
        // need to set up crypto key
        this.seed = this.seed + 1;
        this.focus = false;
      }
    },
    include() {
      // vuetify function to include an element with this class into clickable area without close
      return [document.querySelector(".included")];
    },
  },
};
</script>
