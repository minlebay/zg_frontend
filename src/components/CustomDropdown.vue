<template>
  <div class="custom-dropdown">
    <div class="custom-dropdown-select" @click="toggleDropdown">
      {{ selectedOption }}
      <span class="custom-dropdown-arrow">▼</span>
    </div>
    <div v-if="dropdownOpen" class="custom-dropdown-options">
      <div
          v-for="option in options"
          :key="option"
          class="custom-dropdown-option"
          @click="selectOption(option)"
      >
        {{ option }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    options: {
      type: Array,
      required: true
    },
    value: {
      type: Number,
      required: true
    }
  },
  data() {
    return {
      dropdownOpen: false,
      selectedOption: this.value
    };
  },
  watch: {
    value(newValue) {
      this.selectedOption = newValue;
    }
  },
  methods: {
    toggleDropdown() {
      this.dropdownOpen = !this.dropdownOpen;
    },
    selectOption(option) {
      this.$emit('change', option);
      this.dropdownOpen = false;
      this.selectedOption = option;
    }
  }
};
</script>

<style scoped>
.custom-dropdown {
  position: relative;
  display: inline-block;
  width: 100px;
}

.custom-dropdown-select {
  background-color: #44444444;
  color: #2c3e50;
  margin-left: 3px;
  padding: 8px 8px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease, box-shadow 0.3s ease;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
}

.custom-dropdown-arrow {
  margin-left: 10px;
}

.custom-dropdown-options {
  position: absolute;
  top: 100%;
  left: 0;
  right: 0;
  background-color: #222222;
  border-radius: 4px;
  overflow: hidden;
  z-index: 10;
}

.custom-dropdown-option {
  padding: 8px 16px;
  cursor: pointer;
}

.custom-dropdown-option:hover {
  background-color: #66655545;
}

</style>
