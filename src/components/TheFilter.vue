<template>
  <div class="filter">
    <p>Filter by Alliances</p>
    <div class="checkboxes">
      <label :for="filter.id" v-for="filter in filters" :key="filter.name">
        <input
          type="checkbox"
          :id="filter.id"
          :value="filter.id"
          v-model="selectFilter"
        />
        {{ filter.name }}
      </label>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      filters: [
        {
          id: "OW",
          name: "Oneworld",
        },
        {
          id: "ST",
          name: "Sky Team",
        },
        {
          id: "SA",
          name: "Star Alliance",
        },
      ],
      selectFilter: [],
    };
  },
};
</script>

<style lang="scss">
.filter {
  p {
    font-size: 16px;
    font-weight: bold;
    margin-bottom: 22px;
  }
  .checkboxes {
    display: flex;
    margin-bottom: 56px;
    label {
      display: flex;
      align-items: center;
      font-size: 14px;
      margin-right: 24px;
      input {
        width: 20px;
        height: 20px;
        margin-right: 10px;
      }
    }
  }
}
</style>
