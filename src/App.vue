<template>
  <div id="app">
    <div class="container">
      <div id="bar">
        <h1>Startech Email Template Builder</h1>
        <button v-on:click="exportHtml">Export HTML</button>
      </div>

      <EmailEditor
        ref="emailEditor"
        v-on:load="editorLoaded"
        style="height: 800px"
      />
    </div>
  </div>
</template>

<script>
import { EmailEditor } from "vue-email-editor";
import { saveAs } from "file-saver";

export default {
  name: "app",
  components: {
    EmailEditor,
  },
  methods: {
    editorLoaded() {
      // Pass your template JSON here
      this.$refs.emailEditor.editor.loadDesign({});
    },
    exportHtml() {
      this.$refs.emailEditor.editor.exportHtml((data) => {
        console.log("exportHtml", data);
        const blob = new Blob([data.html], { type: "text/html" });
        saveAs(blob, "email_template.html");
      });
    },
  },
};
</script>
