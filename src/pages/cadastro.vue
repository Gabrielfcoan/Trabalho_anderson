<template>
  <q-page class="bg-grey-3 column">
    <div class="row q-pa-sm bg-primary">
      <q-input
      v-model="addcadastro"
      @keyup.enter="addTask"
      class="col"
      bg-color="white"
      placeholder="Adicionar Tarefa"
      dense>
        <template v-slot:append>
          <q-btn
          @click="addTask"
          round
          dense
          flat
          icon="add" />
        </template>
      </q-input>
    </div>
    <q-list
    class="bg-white"
    separator
    bordered>
      <q-item
      v-for="(task, index) in tasks"
      :key="task.title"
      @click="task.done = !task.done "
      :class="{ 'done bg-clue-1' : task.done }"
      clickable
      v-riple>
        <q-item-section avatar>
          <q-checkbox
          v-model="task.done"
          class="no-pointer-events"
          val="teal"
          color="primary" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{task.title}}</q-item-label>
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
        icon="delete" />
        </q-item-section>
      </q-item>
    </q-list>
    <div
    v-if="!tasks.length"
    class="no-tasks absolute-center">
      <q-icon
      name="check"
      size="100px"
      color="primary"/>
      <div
      class="text-h5 text-primary text-center">
        Tarefas
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  data () {
    return {
      addcadastro: '',
      tasks: [
      ]
    }
  },
  methods: {
    // eslint-disable-next-line space-before-function-paren
    deleteTask(index) {
      this.$q.dialog({
        title: 'Excluir',
        message: 'Confirma a exclusao?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.tasks.splice(index, 1)
        this.$q.notify('Tarefa Excluida')
      })
    },
    // eslint-disable-next-line space-before-function-paren
    addTask() {
      this.tasks.push({
        title: this.addcadastro,
        done: false
      })
      this.addcadastro = ''
    }
  }
}
</script>

<style lang="scss">
  .done {
    .q-item__label {
      text-decoration: line-through;
      color: #bbb;
    }
  }
  .no-tasks {
    opacity: 0.5;
  }
</style>
