<template>
  <header class="c-header">
    <h1 class="c-header__title">Todo</h1>
    <button class="c-header__button"></button>
    <form class="c-header__form" @submit.prevent="add_task">
      <input
        type="text"
        name=""
        id=""
        class="c-header__input"
        placeholder="Create a new todo..."
        v-model="task_model"
      />
      <button type="submit" class="c-header__submit">add</button>
    </form>
  </header>
</template>

<script>
export default {
  name: "HeaderComponent",
  emits: ["toSaveTask"],
  data() {
    return {
      task_model: "",
    };
  },
  methods: {
    add_task() {
      this.$emit("toSaveTask", this.task_model);
      this.task_model = "";
    },
  },
};
</script>

<style lang="scss">
@import "../assets/scss/style.scss";

.container {
  margin: 0 auto;
  max-width: toRem(540);
  padding: toRem(48) toRem(25);
}

.c-header {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;

  &__title {
    color: var(--color-f3);
    font-size: $font-size-md;
    font-weight: $font-weight-xbold;
    letter-spacing: toRem(10);
    text-transform: uppercase;
  }

  &__button {
    width: toRem(30);
    height: toRem(30);
    background-color: transparent;
    background-image: url("https://nasratt.github.io/frontendMentorSolutions/projects/todoList/images/icon-sun.svg");
    background-repeat: no-repeat;
    border: none;
    cursor: pointer;
  }

  &__form {
    display: flex;
    width: 100%;
    margin-top: toRem(40);
    border-radius: toRem(8);
    box-shadow: 0 5px 40px 10px rgba(var(--color-00-rgb), 0.25);
  }

  &__input {
    border: none;
    color: var(--color-ca);
    height: toRem(50);
    flex-grow: 1;
    font-family: inherit;
    font-size: toRem(18);
    padding: toRem(20);
    border-radius: toRem(8) 0 0 toRem(8);
    background-color: var(--color-25);
    caret-color: var(--color-ec);
    outline: none;
  }

  &__submit {
    border: none;
    background-color: var(--color-16);
    color: var(--color-ca);
    padding: 0 toRem(10);
    border-radius: 0 toRem(8) toRem(8) 0;
    text-transform: uppercase;
    cursor: pointer;
  }
}
</style>
