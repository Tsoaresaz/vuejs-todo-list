<template>
  <div class="container">
    <HeaderComponent @toSaveTask="save_task" />
    <main class="main">
      <div class="c-todo-list">
        <ul class="c-todo-list__list">
          <li class="c-todo-list__message">Tasks list is empty!</li>
          <li class="c-todo-list__item" v-for="task of tasks" :key="task.id">
            <input type="checkbox" class="c-todo-list__checkbox" />
            <p class="c-todo-list__text">{{ task.name }}</p>
            <button class="c-todo-list__remove" @click="delete_task(task)">
              <img
                src="https://nasratt.github.io/frontendMentorSolutions/projects/todoList/images/icon-cross.svg"
                alt="Delete task button"
              />
            </button>
          </li>
        </ul>
        <div class="c-todo-list-info">
          <p class="c-todo-list-info__count">
            <span class="c-todo-list-info__number">0</span>
            items left
          </p>
          <button class="c-todo-list-info__button">Clear Completed</button>
        </div>
      </div>
    </main>
  </div>
  <!-- <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </nav>
  <router-view /> -->
</template>

<script>
import HeaderComponent from "@/components/HeaderComponent.vue";

export default {
  name: "App",
  components: {
    HeaderComponent,
  },
  data() {
    return {
      tasks: [
        {
          id: 1,
          name: "Test 01",
        },
        {
          id: 2,
          name: "Test 02",
        },
        {
          id: 3,
          name: "Test 03",
        },
        {
          id: 4,
          name: "Test 04",
        },
        {
          id: 5,
          name: "Test 05",
        },
      ],
    };
  },
  methods: {
    save_task(task) {
      this.tasks.push({
        id: this.tasks.length + 1,
        name: task,
      });
    },
    delete_task(task) {
      console.log("clicked delete: ", task);
      this.tasks = this.tasks.filter((item) => item.id !== task.id);
      console.log("tasks update: ", this.tasks);
    },
  },
};
</script>

<style lang="scss">
@import "./assets/scss/style.scss";

.container {
  margin: 0 auto;
  max-width: toRem(540);
  padding: toRem(48) toRem(25);
}

.c-todo-list {
  $self: &;
  margin-top: toRem(20);
  background-color: var(--color-25);
  border-radius: toRem(8);

  &__item {
    display: flex;
    color: var(--color-ca);
    font-size: toRem(18);
    padding: toRem(15) toRem(20);
    min-height: toRem(55);
    background-color: var(--color-25);
    border-bottom: 1px solid var(--color-39);

    &:hover {
      #{ $self }__remove {
        opacity: 1;
      }
    }
  }

  &__checkbox {
    position: relative;
    display: inline-block;
    margin-right: toRem(30);
    appearance: none;
    cursor: pointer;
    transition: all 0.2s ease-in-out;

    &::before {
      content: "";
      display: inline-block;
      width: toRem(22);
      height: toRem(22);
      border-radius: 50%;
      background: var(--color-39);
      border: 1px solid var(--color-39);
      position: absolute;
      top: 0px;
      left: -4px;
      z-index: 5;
      transition: all 0.2s ease-in-out;
    }

    &::after {
      content: "";
      display: inline-block;
      width: toRem(18);
      height: toRem(18);
      border: none;
      border-radius: 50%;
      background: var(--color-25);
      border: 1px solid var(--color-39);
      position: absolute;
      top: 2px;
      left: -2px;
      z-index: 10;
      transition: all 0.2s ease-in-out;
    }

    &:hover {
      &::before {
        @include backgroundLinear;
      }
    }

    &:checked {
      &::after {
        @include backgroundLinear;
      }
      + #{ $self }__text {
        color: var(--color-39);
        text-decoration: line-through;
      }
    }
  }

  &__text {
    flex-grow: 1;
  }

  &__remove {
    opacity: 0;
    border: none;
    background-color: transparent;
    cursor: pointer;
  }

  &__message {
    color: var(--color-ca);
    padding: toRem(15) toRem(20);
    text-align: center;
  }
}

.c-todo-list-info {
  display: flex;
  justify-content: space-between;
  padding: toRem(20);
  color: var(--color-77);
  font-size: toRem(16);
  border-top: 1px solid var(--color-39);
  transition: all 0.2s ease-in-out;

  &__button {
    color: var(--color-77);
    font-size: toRem(16);
    border: none;
    background-color: transparent;
    cursor: pointer;
    transition: color 0.2s ease-in-out;

    &:hover {
      color: var(--color-ca);
    }
  }
}
</style>
