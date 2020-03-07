<template>
  <v-row>
    <v-col cols="3">
      <v-text-field
        v-model="contry"
        :rules="[() => !required || !!contry || 'Country code is required', () => /^(\+?\d{1,3}|\d{1,4})$/.test(contry) || 'Country code must be valid']"
        label="Country Code"
        append-outer-icon="mdi-minus"
      ></v-text-field>
    </v-col>
    <v-col cols="9" class="pl-0">
      <v-text-field v-model="tel" :rules="[() => !required || !!tel || 'Phone Number is required',() => /^[0-9]*$/.test(tel) || 'Phone Number must be valid']" label="Phone Number" @keypress="isSpace"></v-text-field>
    </v-col>
  </v-row>
</template>

<script>
export default {
  props: {
    value: {
      type: String,
      required: true
    },
    required: {
      type: Boolean,
      required: false,
      default() {
        return false;
      }
    }
  },

  watch: {
    phone(val) {
      this.$emit("input", val);
    },
  },

  computed: {
    phone() {
      return this.contry + this.tel;
    }
  },

  data: () => ({
    contry: "",
    tel: ""
  }),

  methods: {
    isSpace(evt) {
      const { keyCode } = evt
      if(keyCode === 32) evt.preventDefault()
    }
  }
};
</script>

<style lang="scss" scoped>
</style>