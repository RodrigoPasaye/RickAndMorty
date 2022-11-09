<template>
  <div class="pagination">
    <button
      class="button"
      :class="{ disabled: !prevPage }"
      :disabled="!prevPage"
      @click="previous()"
    >
      Previous
    </button>
    <button
      class="button"
      :class="{ disabled: !nextPage }"
      :disabled="!nextPage"
      @click="next()"
    >
      Next
    </button>
  </div>
</template>

<script>
import { useStore } from "vuex";
import { computed } from "vue";

export default {
  setup() {
    const store = useStore();

    const prevPage = computed(() => {
      return store.state.prevPage;
    });
    const nextPage = computed(() => {
      return store.state.nextPage;
    });

    const previous = () => {
      store.dispatch("getPrevPage");
    };

    const next = () => {
      store.dispatch("getNextPage");
    };

    return {
      prevPage,
      nextPage,
      previous,
      next,
    };
  },
};
</script>

<style lang="scss">
.pagination {
  width: 400px;
  margin: 3rem auto 0;
  display: grid;
  grid-template-columns: repeat(2, 1fr);
}
.button {
  background-color: var(--background-card);
  border: none;
  color: white;
  padding: 1rem 0.5rem;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
  -webkit-transition-duration: 0.4s; /* Safari */
  transition-duration: 0.4s;
  &:hover {
    color: var(--text-orange);
  }
}

.button:hover {
  box-shadow: 0 12px 16px 0 rgba(0, 0, 0, 0.24),
    0 17px 50px 0 rgba(0, 0, 0, 0.19);
}

.disabled {
  opacity: 0.6;
  cursor: not-allowed;
}
</style>
