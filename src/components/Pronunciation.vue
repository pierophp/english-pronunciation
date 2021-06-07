<template>
  <div>
    <div>
      <button v-on:click="generate">Gerar</button>
    </div>
    <div><textarea v-model="text"></textarea></div>
    <div v-for="line in parsedLines" :key="line.id">
      <span v-for="block in line.blocks" :key="block.id">
        <ruby>
          <rb>{{ block.text }}</rb
          ><rt>{{ block.pronunciation }}</rt>
        </ruby>
        {{ " " }}
      </span>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

type ParsedBlock = Array<{
  id: number;
  text: string;
  pronunciation?: string;
}>;

type ParsedLines = Array<{
  id: number;
  blocks: ParsedBlock;
}>;

const dictionary: { [code: string]: string } = {
  my: "mī,mə",
  name: "ˈnām",
  is: "",
};

export default defineComponent({
  name: "Pronunciation",
  data() {
    const parsedLines: ParsedLines = [];
    return {
      text: "",
      parsedLines,
    };
  },
  methods: {
    generate() {
      const lines = this.text.split("\n");
      const parsedLines: ParsedLines = [];
      let i = 0;

      for (const line of lines) {
        const parsedBlocks: ParsedBlock = [];
        const blocks = line.split(" ");

        let j = 0;
        for (const block of blocks) {
          parsedBlocks.push({
            id: j,
            text: block,
            pronunciation: dictionary[block.toLowerCase()] ?? "",
          });
          j++;
        }

        parsedLines.push({
          id: i,
          blocks: parsedBlocks,
        });
        i++;
      }

      console.log(parsedLines);

      this.parsedLines = parsedLines;
    },
  },
  setup: () => {},
});
</script>

<style scoped></style>
