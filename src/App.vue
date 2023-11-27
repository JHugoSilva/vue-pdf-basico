<script setup>
import HelloWorld from "./components/HelloWorld.vue";

import pdfMake from "pdfmake/build/pdfmake";
import * as pdfFonts from "pdfmake/build/vfs_fonts";

pdfMake.vfs = pdfFonts.pdfMake.vfs;

const exportPdf = () => {
  let animals =  [[ 'First', 'Second', 'Third', 'The last one' ],
          [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
          [ { text: 'Bold value', bold: true }, 'Val 2', 'Val 3', 'Val 4' ]]

   let docDefinition = {
        content: [
          {
            layout: "lightHorizontalLines", // optional
            table: {
              // headers are automatically repeated if the table spans over multiple pages
              // you can declare how many rows should be treated as headers
              headerRows: 1,
              widths: ["*", "auto", 100, "*"],

              body: animals
            },
          },
        ],
      };
      const pdf = pdfMake.createPdf(docDefinition)
      pdf.print()
    }

// export default {
//   name: "App",
//   components: {
//     HelloWorld,
//   },
//   data() {
//     return {
//       animals: [["Column 1", "Column 2", "Column 3", "Column 4"]],
//     };
//   },
//   methods: {
//     exportPdf() {
//       let docDefinition = {
//         content: [
//           {
//             layout: "lightHorizontalLines", // optional
//             table: {
//               // headers are automatically repeated if the table spans over multiple pages
//               // you can declare how many rows should be treated as headers
//               headerRows: 1,
//               widths: ["*", "auto", 100, "*"],

//               body: this.animals
//             },
//           },
//         ],
//       };
//       const pdf = pdfMake.createPdf(docDefinition)
//       pdf.open()
//     },
//   },
// };
</script>

<template>
  <div>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <HelloWorld msg="Vite + Vue" />
  <button @click="exportPdf">Pdf</button>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
