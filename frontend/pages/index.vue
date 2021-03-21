<template>
  <div>
    <div>
      Resolved:
      <div>
        hellloosdv why is empty
      </div>
    </div>
    <div>
      Unresolved:
      <div v-for="error in unresolved">`{{ error.code }}`</div>
    </div>
    <div>
      Backlog:
      <div v-for="error in backlog">`{{ error.code }}`</div>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios }) {
    try {
      const { resolved, unresolved, backlog } = await $axios.$get(
        "http://localhost:8000/get_lists"
      );
      return {
        resolved,
        unresolved,
        backlog
      };
    } catch (error) {
      console.log(
        `Couldn't get error lists:\n${error}\nDid you start the API?`
      );
      console.log(
        "HINT: You can comment out the full `asyncData` method and work with mocked data for UI/UX development, if you want to."
      );
    }
  },
  data() {
    return {
      resolved: [],
      unresolved: [],
      backlog: []
    };
  }
};
</script>
