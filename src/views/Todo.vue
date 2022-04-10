<template>
  <div class="home">
    <v-text-field
      class="pa-3"
      outlined
      label="Add Task"
      append-icon="mdi-map-marker"
    ></v-text-field>
    <v-list class="pt-0" flat>
      <div v-for="task in tasks" :key="task.id">
        <v-list-item
          @click="doneTask(task.id)"
          :class="{ 'cyan lighten-5': task.done }"
        >
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox :input-value="task.done" color="primary"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
                :class="{ 'text-decoration-line-through': task.done }"
                >{{ task.title }}</v-list-item-title
              >
            </v-list-item-content>

            <v-list-item-action>
              <v-btn @click.stop="deleteTask(task.id)" icon>
                <v-icon color="primary lighten-1">mdi-delete</v-icon>
              </v-btn>
            </v-list-item-action>
          </template>
        </v-list-item>
        <v-divider></v-divider>
      </div>
    </v-list>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      tasks: [
        {
          id: 1,
          title: "Work out",
          done: false,
        },
        {
          id: 2,
          title: "Study JavaScript",
          done: false,
        },
        {
          id: 3,
          title: "Take Coffee",
          done: false,
        },
      ],
    };
  },
  methods: {
    doneTask(id) {
      // filter함수는 하나의 object가 아닌 array를 반환하므로, [0]을 포함시킴
      let task = this.tasks.filter((task) => task.id === id)[0];
      task.done = !task.done;
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },
  },
};
</script>
