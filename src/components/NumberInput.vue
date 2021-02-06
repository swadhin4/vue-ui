<template>
  <v-text-field
      v-model="price"
      ref="field"
      type="text"
      :rules="priceRules"
      label="Price"
      required
    ></v-text-field>
</template>

<script>
import AutoNumeric from "autonumeric";

export default {
  name: "NumberInput",
  mounted() {
    new AutoNumeric(this.$refs.field.$refs.input);
  },
  data: () => {
    return {
      valid: true,
      price: '',
      priceRules: [
        v => !!v || 'Price is required'
      ],
    };
  }
};
</script>