<template lang="html">
  <div class="basic-demo">
    <h1>All Demo</h1>
      <vue-tags-input
        class="tags-input"
        v-model="tag"
        :tags="tags"
        :add-on-key="[188, 186, 13]"
        :save-on-key="[188, 38, 13]"
        :allow-edit-tags="true"
        :separators="[',']"
        :autocomplete-items="autocompleteItems"
        @tags-changed="newTags => tags = newTags">
      </vue-tags-input>
  </div>
</template>

<script>
import VueTagsInput from '../../vue-tags-input/vue-tags-input';

export default {
  name: 'ToDevelop',
  components: {
    VueTagsInput,
  },
  data() {
    return {
      tag: '',
      tags: [{
        text: 't1',
        classes: 'test',
      }, {
        text: 't5',
      }],
      validation: [{
        type: 'min-length',
        rule: '^.{4,}$',
      }, {
        type: 'only-numbers',
        rule: '[0-9]',
      }],
      countries: [
        'Germany', 'Holland', 'France', '09879', 't1', 't1',
      ],
      autocompleteItems: [],
    };
  },
  methods: {
    tagClicked(obj) {
      console.log(obj);
    },
    test(i) {
      console.log(i);
    },
    foundDuplicate(tag) {
      console.log(tag);
    },
    decideDeleting(obj) {
      obj.deleteTag(true);
    },
    decideEdit(obj) {
      obj.editTag(true);
    },
    decideAdding(obj) {
      obj.addTag(true);
    },
    decideSaving(obj) {
      obj.saveTag(true);
    },
    addInvalidOnPurpose(tag) {
      this.tags.push(tag);
    },
    setAutocompleteItems() {
      // if (this.tag.length === 0) return this.autocompleteItems = [];
      this.autocompleteItems = this.countries
        .filter(c => c.toLowerCase().indexOf(this.tag.toLowerCase()) !== -1)
        .map(text => {
          return { text, test: 'nlub' };
        });
    },
    addTag() {
      this.tags.push({ text: ('hu') });
    },
  },
  watch: {
    tag: 'setAutocompleteItems',
  },
  mounted() {
    this.setAutocompleteItems();
  },
};
</script>

<style lang="scss">
@import '~colors';

.basic-demo .tag.duplicate {
  background-color: #141f2d;
}

.basic-demo .tag.invalid.only-numbers {
  background-color: $warn;
}

.basic-demo .new-tag-input.invalid.min-length {
  color: $error;
}

.basic-demo .new-tag-input.invalid.only-numbers {
  color: $warn;
}
</style>
