<template>
  <base-checkbox
    @change="changeUncoveredByRules"
    class="checkbox--dark"
    :value="filter.selected"
  >
    Only records not covered by rules
  </base-checkbox>
</template>

<script>
import { TextClassificationDataset } from "@/models/TextClassification";
export default {
  props: {
    dataset: {
      type: TextClassificationDataset,
      required: true,
    },
    filter: {
      type: Object,
      required: true,
    },
  },
  methods: {
    async changeUncoveredByRules() {
      const rulesId = this.dataset.rules.map((r) => r.query);
      this.$emit("apply", this.filter, !this.filter.selected ? rulesId : []);
    },
  },
};
</script>

<style lang="scss" scoped>
.checkbox {
  flex-direction: row-reverse;
  margin-left: 2em;
  @include font-size(13px);
  :deep(.checkbox-label) {
    margin-left: $base-space;
  }
}
</style>
