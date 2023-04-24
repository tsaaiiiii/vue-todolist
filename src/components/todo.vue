<template>
  <div class="todo_list">
    <div class="title">
      <h1 class="h1">ToDo List</h1>
      <p>
        Yesterday is history, tomorrow is a mystery, but
        <span>today is a gift.</span>
      </p>
    </div>

    <div class="newThing">
      <input
        type="text"
        class="todoAdd"
        placeholder="What are you doing today？"
        v-model="this.add.todo.content"
      />
      <input type="button" class="btn" value="sent" @click="sent_btn" />
    </div>

    <div class="allBtn">
      <input type="button" class="all" value="All" @click="showType = 'all'" />
      <input
        type="button"
        class="finished"
        value="Finished"
        @click="showType = 'Finished'"
      />
      <input
        type="button"
        class="pending"
        value="Pending"
        @click="showType = 'Pending'"
      />
    </div>
    <ul class="list">
      <li v-for="item in filteredData" :key="item.id">
        <p>{{ item.content }}</p>
        <input
          type="checkbox"
          class="check"
          value="✔"
          v-bind:checked="item.selected"
          @click="patch_check(item)"
        /><input
          type="button"
          class="delete"
          value="✘"
          @click="delete_btn(item)"
        />
      </li>
    </ul>
    <div><h3></h3></div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      apiEndpoint: "https://todoo.5xcamp.us/todos",
      add: {
        todo: {
          content: "",
        },
      },
      config: {
        headers: {
          Authorization: localStorage.getItem("userToken"),
          accept: "application/json",
        },
      },
      data: [],
      showType: "all",
    };
  },
  methods: {
    // 初始
    init() {
      axios.get(this.apiEndpoint, this.config).then((res) => {
        console.log(res);
        this.data = res.data.todos;
        // console.log(this.data);
        this.data.forEach((item) => {
          if (item.completed_at !== null) {
            item.selected = true;
          }
        });
      });
    },

    // 新增
    sent_btn() {
      axios
        .post(this.apiEndpoint, this.add, this.config)
        .then((res) => {
          console.log(res);
          //  console.log(this.token);
          alert("add successful！");
          this.add.todo.content = "";
          this.init();
        })
        .catch((err) => {
          console.log(err);
        });
    },
    // 刪除
    delete_btn(item) {
      axios
        .delete(`${this.apiEndpoint}/${item.id}`, this.config)
        .then((res) => {
          console.log(res);
          alert("delete successful！");
          this.init();
        })
        .catch((error) => {
          console.log(error);
        });
    },
    // 修改
    patch_check(item) {
      axios
        .patch(`${this.apiEndpoint}/${item.id}/toggle`, {}, this.config)
        .then((res) => {
          console.log(res);
          this.init();
        })
        .catch((error) => {
          console.log(error);
        });
    },
    // 全部
  },
  computed: {
    filteredData() {
      if (this.showType === "Finished") {
        return this.data.filter((item) => item.completed_at !== null);
      } else if (this.showType === "Pending") {
        return this.data.filter((item) => item.completed_at === null);
      } else {
        return this.data;
      }
    },
  },

  mounted() {
    this.init();
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
li {
  height: 28px;
  text-align: left;
  display: flex;
  justify-content: center;
  font-size: 20px;
  align-items: center;
}
.newThing {
  margin-bottom: 20px;
}
</style>
