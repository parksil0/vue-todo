<script lang="ts">
import Layout from "../components/Layout/index.vue";
import CheckIcon from "../components/svgs/Check.vue";
import TrashIcon from "../components/svgs/Trash.vue";

interface TodoItem {
  title: string;
  description: string;
  isFinished: boolean;
}

export default {
  components: {
    Layout,
    CheckIcon,
    TrashIcon,
  },
  data() {
    return {
      todoItems: [] as TodoItem[],
      errorMessage: {
        title: "",
        description: "",
      },
      title: "",
      description: "",
    };
  },
  methods: {
    onSubmit() {
      const { title, description } = this;

      if (!description) {
        this.errorMessage.description = "설명을 입력해주세요.";
        (this.$refs.description as HTMLInputElement).focus();
      }

      if (description) {
        this.errorMessage.description = "";
      }

      if (!title) {
        this.errorMessage.title = "타이틀을 입력해주세요.";
        (this.$refs.title as HTMLInputElement).focus();
      }

      if (title) {
        this.errorMessage.title = "";
      }

      if (this.todoItems.find((todoItem) => todoItem.title === title)) {
        this.errorMessage.title = "이미 존재하는 타이틀입니다.";
        (this.$refs.title as HTMLInputElement).focus();
      }

      if (this.errorMessage.title || this.errorMessage.description) {
        return;
      }

      const todoItem = {
        title,
        description,
        isFinished: false,
      };

      this.todoItems.push(todoItem);

      this.title = "";
      this.description = "";
      (this.$refs.title as HTMLInputElement).focus();
    },
    onClickCheckButton(title: string) {
      const todoItem = this.todoItems.find(
        (todoItem) => todoItem.title === title
      );

      if (todoItem) {
        todoItem.isFinished = !todoItem.isFinished;
      }
    },
    onClickDeleteButton(title: string) {
      if (!confirm(`정말 ${title}을(를) 삭제하시겠습니까?`)) {
        return;
      }

      this.todoItems = this.todoItems.filter(
        (todoItem) => todoItem.title !== title
      );
    },
    getTextDecoration(isFinished: boolean) {
      return isFinished ? "line-through" : "none";
    },
  },
};
</script>

<template>
  <Layout>
    <form class="form" @submit.prevent="onSubmit">
      <div>
        <label class="label" for="title">제목</label>
        <input
          ref="title"
          id="title"
          class="input"
          type="text"
          v-model="title"
        />
        <p class="error-message" v-if="Boolean(errorMessage.title)">
          {{ errorMessage.title }}
        </p>
      </div>
      <div>
        <label class="label" for="description">설명</label>
        <input
          ref="description"
          id="description"
          class="input"
          type="text"
          v-model="description"
        />
        <p class="error-message" v-if="Boolean(errorMessage.description)">
          {{ errorMessage.description }}
        </p>
      </div>
      <button class="button" type="submit">추가하기</button>
    </form>

    <div class="todo-item" v-for="todoItem in todoItems" :key="todoItem.title">
      <div class="todo-item__title">
        <div class="todo-item__title-left">
          <button @click="onClickCheckButton(todoItem.title)">
            <CheckIcon v-bind:isFinished="todoItem.isFinished" />
          </button>
          <p
            :style="{
              'text-decoration': getTextDecoration(todoItem.isFinished),
              color: todoItem.isFinished ? '#C4C4C4' : 'black',
            }"
          >
            {{ todoItem.title }}
          </p>
        </div>

        <button @click="onClickDeleteButton(todoItem.title)">
          <TrashIcon />
        </button>
      </div>
      <p
        class="todo-item__description"
        :style="{
          'text-decoration': getTextDecoration(todoItem.isFinished),
          color: todoItem.isFinished ? '#C4C4C4' : 'black',
        }"
      >
        {{ todoItem.description }}
      </p>
    </div>
  </Layout>
</template>

<style scoped>
.label {
  font-size: 14px;
  line-height: 21px;
  color: #333333;
  margin-left: 8px;
}
.input {
  width: 100%;
  height: 48px;
  padding: 0 24px;
  border-radius: 8px;
  font-size: 16px;
  line-height: 24px;
  color: #333333;
  background-color: #a8d2a5;
  border: 2px solid #a8d2a5;
  outline: none;

  transition: all 0.1s ease-in-out;
}

.form {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 16px;
}

.form div {
  width: 100%;
}

.input::placeholder {
  font-weight: lighter;
}

.input:hover {
  border-color: #bfdcbd;
}

.input:focus {
  border-color: #77a374;
}

.error-message {
  font-size: 12px;
  line-height: 18px;
  color: #ff0000;
  margin-top: 4px;
}

.button {
  width: 290px;
  height: 60px;
  border-radius: 25px;
  font-size: 18px;
  line-height: 29px;
  color: #333333;

  background: linear-gradient(90deg, #a8d2a5 0%, #acd4e1 115.2%);

  transition: all 0.2s ease-in-out;
}

.button:hover {
  box-shadow: 3px 3px 3px #acd4e1;
}

.button:active {
  box-shadow: 1px 1px 1px #acd4e1;
}

.todo-item {
  width: 100%;

  display: flex;
  flex-direction: column;
}

.todo-item__title {
  border-bottom: 2px solid #3e3b3b;
  display: flex;
  justify-content: space-between;
  padding-bottom: 4px;
  padding-right: 24px;
}

.todo-item__title-left {
  display: flex;
  align-items: center;
  gap: 16px;
}

.todo-item__description {
  font-size: 14px;
  line-height: 23px;
}
</style>
