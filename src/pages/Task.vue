<template>
  <q-page class="bg-grey-3 column">
    <div class="row q-pa-sm bg- color-primary">
      <q-input
      v-model="newTask"
      @keyup.enter="addTask"
      class="col"
      square
      filled
      bg-color="white"
      placeholder="Adicionar tarefa"
      dense>
      <template v-slot:append>
        <q-btn
        @click="addTask"
        round
         dense
         flat
         icon="add"/>

      </template>
    </q-input>
    </div>
 <q-list  class="bg-white"
separator
bordered

 >
  <q-item
  v-for="(task, index) in tasks"
  :key="task.tittle"
  @click="task.done = !task.done"
  :class="{'done bg-green-1' : task.done}"
  clickable
  v-ripple>
    <q-item-section avatar>
      <q-checkbox
      v-model="task.done"
      class="no-pointer-events"
      color="primary"/>
    </q-item-section>
  <q-item-section>
  <q-item-label>{{ task.title }}</q-item-label>
  </q-item-section>
  <q-item-section
  v-if="task.done"
  side>
  <q-btn
  @click.stop="deleteTask(index)"
  flat
  round
  dense
  color="primary"
  icon="delete"/>
  </q-item-section>

  </q-item>
 </q-list>
 <div
 v-if="!tasks.length"
 class="no-tasks absolute-center">
  <q-icon name="check"
  size="100px"
  color="green" />
<div class="text-h5 text-primary text-center">
  Sem Tarefas
</div>

 </div>
  </q-page>
</template>

<script>
import {defineComponent} from "vue";

export default defineComponent({
  name: "TaskPage",

  data() {
    return {
      newTask: "",
      tasks: JSON.parse(localStorage.getItem("tasks")) || [],
    };
  },
  methods: {
    deleteTask(index) {
      this.$q
        .dialog({
          title: "Confirmação",
          message: "Deseja eliminar este item?",
          cancel: true,
          persistent: true,
        })
        .onOk(() => {
          this.tasks.splice(index, 1);
          localStorage.setItem("tasks", JSON.stringify(this.tasks));
          this.$q.notify("Item eliminado com sucesso!");
        });
    },
    addTask() {
      this.tasks.push({
        title: this.newTask,
        done: false,
      });
      this.newTask = "";
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },
  },
});


</script>

<style lang="scss">
.done{
.q-item_label{
  text-decoration: line-through;
  color: rgba(109, 138, 7, 0.671);
}

.no-task{
  opacity: 0.5;
}

}
</style>
